# RSA File Cipher

TQ uses RSA PKCS#1 2048-bit asymmetric encryption to protect some game data files. This page explains how the cipher works and how to decrypt these files.

> ⚠️ __WARNING__
>
> Some data files use a different encryption/decryption method. This cipher only decrypts & encrypts files marked as 'RSA' on [DAT](../files/formats/dat.md). Other encryption types like TQ File Cipher will not work with this method.

> ℹ️ __Information__
>
> **All information on this page is derived from the publicly distributed client binaries. The extracted key is an RSA public key and therefore is public by design.**

## Table of Contents

- [Cipher Overview](#cipher-overview)
- [Extracting Public Key](#extracting-public-key)
  - [Example Extracted Deobfuscated Modulus](#example-extracted-deobfuscated-modulus)
- [Decryption](#decryption)
- [Encryption](#encryption)


## Cipher Overview

TQ first gzip-compresses then encrypts the file using their **2048-bit RSA private key** when the client is compiled. The client has the **public key** baked into the binary and uses it to decrypt the file then decompress it.

It's possible to extract the public key from the client binary to decrypt the files. However, without the original private key, it is not possible to re-encrypt the file. Instead, the alternative is to patch the client binary (see [Encryption](#encryption))

The compressed & encrypted file is split into 256-byte ciphertext blocks. Each block is decrypted with the public key then concatenated together & decompressed.

## Extracting Public Key

The client binary obfuscates the baked-in public key. Rather than storing it as plain PEM format, the 2048-bit modulus is stored as 64 uint32 words in an obfuscated form, reconstructed at runtime by a rolling forward XOR of adjacent elements.

In the binary, the constructor of `CConfigMgr` reconstructs the public key. First by fetching a static constant array of 64 uint32 words, then applying a rolling XOR over adjacent elements to reconstruct the 64 modulus words, which are passed to statically linked OpenSSL RSA functions along with the fixed, standard exponent `65537` to construct the public key.

In the Mac binary, the 64 uint32 words are stored a contiguous static array, making it very easy to extract. However, in the Windows binary, they are not contiguous but use a mix of `mov` instructions (still extractable but not as easy).

Below is a script which can deobfuscate the public key. You must supply it the 64 uint32 obfuscated modulus words which can be found in the client binary in the CConfigMgr constructor.

```python
obfuscated = [ 0x..., 0x..., 0x..., ... ] # Replace this with the extracted 64 uint32 obfuscated modulus words from binary in CConfigMgr constructor.

modulus_words = [0] * 64

# Rolling XOR
idx = 17 # Starting position for XOR loop (hardcoded in binary)
for j in range(63):
    modulus_words[idx % 64] = obfuscated[j] ^ obfuscated[j + 1]
    idx += 1
modulus_words[idx % 64] = obfuscated[63]

# Assemble into a single 2048-bit integer (Deobfuscated RSA Modulus n)
n = 0
for w in modulus_words:
    n = (n << 32) | w
e = 65537 # Standard RSA public exponent
```

### Example Extracted Deobfuscated Modulus

To verify your extraction using the above process was successful. You can compare your extraction output with the expected deobfuscated RSA modulus (`n`) verified on patch **5517** as a 512-character hex string:

```
bef5bd339b6bac0c957fa68ec010a7d7c38a2b03a9d2084f0e107b2644e246b3
fab03ac76235ae40a0731714783d49caa99ac78a8a39d8b944f168b3aea3b216
2220f2a7444735e07e70a66dd7843c899b64e6a5ee88e4f87b255c2395299899
296e043ea19b6b9b38dfbf671a80a77693fedc7030be7b241726d208010a8dd3
9780e60c2d47dedaa720f56517657eed9e88fe1c9b37591599210ab095e4c251
bd9ea7faf4450cb15a5078a2093cf112e99f34648154d2cc94c38392d724f0fa
fc629e70cd1b97ee4eb82c11c2b0954cef918560ef9f2c7da60b33e767f5d626
cd3d0a6082a06650e54926be71b66e39c33b6e18b7c703830b87a2e4d8805409
```

This deobfuscated RSA modulus (`n`) is likely to be the same on other patches, but only **5517** was tested.


## Decryption

With the public key extracted, we can now decrypt the game files via this process:

1. Split the encrypted data file into 256-byte ciphertext blocks.
2. For each block, standard RSA public-decrypt: `chunk = pow(c, e, n)` (`c` = a 256-byte ciphertext block, `e` = the exponent (65537), `n` = the deobfuscated RSA modulus)
3. Strip the PKCS#1 padding from the decrypted chunk
4. Concatenate all decrypted chunks.
5. Gzip-decompress the concatenated payload.

This script takes an encrypted game data file as `arg1`.

The following snippet implements the above logic in python. This script has **no error handling, checks or dependencies** as it is intentionally minimal for readability.

The result will be written to the same directory as the encrypted file with the appendix `_decrypted`, if the decrypted file already exists it will be overwritten!

```python
import sys, zlib

# Replace n with deobfuscated RSA modulus. Below is from patch 5517 (but likely suitable for all other patches)
n = int("bef5bd339b6bac0c957fa68ec010a7d7c38a2b03a9d2084f0e107b2644e246b3"
        "fab03ac76235ae40a0731714783d49caa99ac78a8a39d8b944f168b3aea3b216"
        "2220f2a7444735e07e70a66dd7843c899b64e6a5ee88e4f87b255c2395299899"
        "296e043ea19b6b9b38dfbf671a80a77693fedc7030be7b241726d208010a8dd3"
        "9780e60c2d47dedaa720f56517657eed9e88fe1c9b37591599210ab095e4c251"
        "bd9ea7faf4450cb15a5078a2093cf112e99f34648154d2cc94c38392d724f0fa"
        "fc629e70cd1b97ee4eb82c11c2b0954cef918560ef9f2c7da60b33e767f5d626"
        "cd3d0a6082a06650e54926be71b66e39c33b6e18b7c703830b87a2e4d8805409", 16) # Hex-String to Int
e = 65537

filename = sys.argv[1]
name, ext = filename.rsplit(".", 1)
out_filename = name + "_decrypted." + ext

with open(filename, "rb") as f:
    data = f.read()

# Decrypt each 256 chunk in big endian & remove any padding
payload = b""
for i in range(0, len(data), 256):
    ciphertext_block = int.from_bytes(data[i:i + 256], byteorder="big")
    chunk = pow(ciphertext_block, e, n).to_bytes(256, byteorder="big")
    padding_end = chunk.index(b"\x00", 2) # Locate end of PKCS#1 padding
    payload += chunk[padding_end + 1:]

with open(out_filename, "wb") as f:
    f.write(zlib.decompress(payload, wbits=47)) # Gzip decompress
```

Example: `python3 co_rsa_decrypt.py server.dat`

## Encryption

Re-encrypting the file is not possible without TQ's private key. Some possible solutions, but out of scope for this page are:

* Generate your own RSA 2048-bit keypair, encrypt the files with your private key, and patch the client binary to replace the obfuscated modulus with your own.
* Patch the binary to skip RSA decryption entirely, so files are read as plaintext.