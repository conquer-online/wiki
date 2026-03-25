# TQ File Cipher

TQ uses a symmetric file cipher used to encrypt & decrypt some data files. This page explains how to decrypt and encrypt game data files using this cipher.


> ⚠️ __WARNING__
>
> Some data files use a different encryption/decryption method. This cipher only decrypts & encrypts files marked as 'TQ File Cipher' on [DAT](../files/formats/dat.md). Other encryption types like RSA will not work with this method.

## Table of Contents

- [Cipher Overview](#cipher-overview)
- [Example Scripts](#example-scripts)
  - [Decryption](#decryption)
  - [Encryption](#encryption)

## Cipher Overview

This cipher uses Microsoft's classic `rand()` algorithm, called "Linear Congruential Generator" (LCG) to generate pseudorandom numbers as the key, so using the same seed value will produce the same output (set of random numbers) every time. For each byte, the cipher then performs an XOR with the key & a bitrotate to decrypt (the inverse to encrypt).

In order to decrypt or encrypt the data file, we need to know the seed value. The seed is hardcoded in the client binary, but a list can be found in: [DAT](../files/formats/dat.md) 


**Key Generation** 

The key size is hardcoded in the client binary, it is `128`. The key bytes will **always** be the same value when given the same seed. With the seed, we can derive the 128 independent key bytes by implementing Microsoft's classic `rand`:

```
n = seed * 0x343FD + 0x269EC3
seed = n & 0xFFFFFFFF
key[i] = ((n >> 16) & 0x7FFF) % 0x100
```

We now have a key[128], where each element in the array is a value 0-255 (a byte).

We then process the file **byte-by-byte**:

**To Decrypt Each Byte**:
1. XOR the byte with `key[i % 128]`
2. Right rotate the byte by `i % 8` bits

**To Encrypt Each Byte**:
1. Left Rotate the byte by `i % 8` bits
2. XOR with `key[i % 128]`


## Example Scripts

The following snippets implement the above logic in python. These scripts have **no error handling, checks or dependencies** as they are intentionally minimal for readability.


### Decryption

This script takes a encrypted game data file as `arg1` and the seed value as `arg2` in either decimal (9527) or hex (0x2537). The seeds for each file can be found in: [DAT](../files/formats/dat.md). It is important to use the correct seed value, otherwise the decrypted output will be garbled.

The result will be written to the same directory as the encrypted file with the appendix `_decrypted`, if the decrypted file already exists it will be overwritten!


```python
import sys

filename = sys.argv[1]
seed = int(sys.argv[2], 0)
name, ext = filename.rsplit(".", 1)
out_filename = name + "_decrypted." + ext
key_size = 128

# Step 1: Key Generation
key = []
for _ in range(key_size):
    n = seed * 0x343FD + 0x269EC3
    seed = n & 0xFFFFFFFF
    key.append(((n >> 16) & 0x7FFF) % 0x100)

data = open(filename, "rb").read()

# Step 2: Byte-for-byte of the file
result = []
for i in range(len(data)):
    b = data[i]
    xored = b ^ key[i % key_size] # XOR byte with key byte
    rotated = ((xored >> (i % 8)) | (xored << (8 - i % 8))) & 0xFF # Right Rotate
    result.append(rotated)

open(out_filename, "wb").write(bytes(result))
```

Example: `python3 tqdecrypt.py magictypeop.dat 9527`

### Encryption

This script takes an unencrypted game data file as `arg1` and seed value as `arg2` in either decimal (9527) or hex (0x2537). The seeds for each file can be found in: [DAT](../files/formats/dat.md). It is important to use the correct seed value, otherwise the client will not be able to decrypt the file and throw an error.

The result will be written to the same directory as the encrypted file with the appendix `_encrypted`, if the encrypted file already exists it will be overwritten!


```python
import sys

filename = sys.argv[1]
seed = int(sys.argv[2], 0)
name, ext = filename.rsplit(".", 1)
out_filename = name + "_encrypted." + ext
key_size = 128

# Step 1: Key Generation
key = []
for _ in range(key_size):
    n = seed * 0x343FD + 0x269EC3
    seed = n & 0xFFFFFFFF
    key.append(((n >> 16) & 0x7FFF) % 0x100)

data = open(filename, "rb").read()

# Step 2: Byte-for-byte of the file
result = []
for i in range(len(data)):
    b = data[i]
    rotated = ((b >> (8 - i % 8)) + (b << (i % 8))) & 0xFF  # Left Rotate
    result.append(rotated ^ key[i % key_size])  # XOR byte with key byte

open(out_filename, "wb").write(bytes(result))
```

Example: `python3 tqencrypt.py magictypeop.dat 9527`
