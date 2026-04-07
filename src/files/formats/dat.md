# DAT

A DAT file is generic data. DAT files are either plain-text, binary-encoded, or encrypted. This page lists the DAT files in the client patch version and an overview of how to read them. For an explanation of what each file does, see its individual linked page.

## DAT File Formats Summary

* [**TQ File Cipher**](../../security/tqfile.md): Files which are marked as encrypted by TQ File Cipher. These files can be decrypted & re-encrypted. The seed for each file is listed in brackets.

* **RSA**: Files which are marked RSA have been encrypted by a TQ 2048-bit RSA private key. The public key is baked and obfuscated in the client binary. While it's possible to extract the public key from the binary to decrypt the file, it is not possible to re-encrypt without the private key.

* **SWF**: Files which are marked SWF are actually a SWF file (Shockwave Flash). Rename the extension to SWF. jpexs-decompiler is a good & free decompiler for this file type.
 
* **Binary Encoded**: The file is unencrypted, but has a binary structure. A hex editor can be used to inspect the raw binary contents but a dedicated parser is required to read it correctly. See the individual linked dat file for more information.

* **Unencrypted - Plain Text**: The file is unencrypted, you should be able to open the file in notepad without issues.

## Patch 5517

| File (relative to client root)                                  | DAT Format                                                              |
|-----------------------------------------------------------------|-------------------------------------------------------------------------|
| [./AutoPatch.dat](../content/autopatch.dat)                     | Unencrypted - Plain Text                                                |
| [./ini/UserHelpInfo.dat](../content/userhelpinfo.dat)           | TQ File Cipher (Seed: 9527 / 0x2537)                                    |
| [./ini/Action.dat](../content/action.dat)                       | Unknown & No references to it (Unused?)                                 |
| [./ini/Monster.dat](../content/monster.dat)                     | TQ File Cipher (Seed: 9527 / 0x2537)                                    |
| [./ini/GameMap.dat](../content/gamemap.dat)                     | Binary Encoded                                                          |
| [./ini/AutoAllot.dat](../content/autoallot.dat)                 | Unknown & No references to it (Unused?)                                 |
| [./ini/MyAnimate.dat](../content/myanimate.dat)                 | RSA Encrypted                                                           |
| [./ini/LevelExp.dat](../content/levelexp.dat)                   | Unknown & No references to it (Unused?)                                 |
| [./ini/Shop.dat](../content/shop.dat)                           | Unencrypted - Plain Text                                                |
| [./ini/Play.dat](../content/play.dat)                           | Custom Encrypted: Subtract 6 from each byte (Used in play.exe launcher) |
| [./ini/ShowHandTable.dat](../content/showhandtable.dat)         | RSA Encrypted                                                           |
| [./ini/suittype.dat](../content/suittype.dat)                   | RSA Encrypted                                                           |
| [./ini/RaceTrackProp.dat](../content/racetrackprop.dat)         | RSA Encrypted                                                           |
| [./ini/magictypeop.dat](../content/magictypeop.dat)             | TQ File Cipher (Seed: 9527 / 0x2537)                                    |
| [./ini/slient.dat](../content/slient.dat)                       | TQ File Cipher (Seed: 9527 / 0x2537)                                    |
| [./ini/mounttype.dat](../content/mounttype.dat)                 | TQ File Cipher (Seed: 9527 / 0x2537)                                    |
| [./ini/levexp.dat](../content/levexp.dat)                       | TQ File Cipher (Seed: 1234 / 0x04D2)                                    |
| [./ini/tqist.dat](../content/tqist.dat)                         | Unknown (Referenced in ndist.dll)                                       |
| [./ini/UserHelpInfo.ini.dat](../content/userhelpinfo.ini.dat)   | TQ File Cipher (Seed: 9527 / 0x2537)                                    |
| [./ini/MagicType.dat](../content/magictype.dat)                 | TQ File Cipher (Seed: 9527 / 0x2537)                                    |
| [./ini/showhandlayout.dat](../content/showhandlayout.dat)       | RSA Encrypted                                                           |
| [./ini/itemtype.dat](../content/itemtype.dat)                   | TQ File Cipher (Seed: 9527 / 0x2537)                                    |
| [./ini/MapDestination.dat](../content/mapdestination.dat)       | TQ File Cipher (Seed: 9527 / 0x2537)                                    |
| [./ini/Tips.dat](../content/tips.dat)                           | Binary Encoded                                                          |
| [./version.dat](../content/version.dat)                         | Unencrypted - Plain Text                                                |
| [./res.dat](../content/res.dat)                                 | Unencrypted - Plain Text                                                |
| [./Server.dat](../content/server.dat)                           | RSA Encrypted                                                           |
| [./data/main/start.dat](../content/start.dat)                   | SWF - Shockwave Flash File                                              |
| [./data/main/role.dat](../content/role.dat)                     | SWF - Shockwave Flash File                                              |
| [./data/main/start-facebook.dat](../content/start-facebook.dat) | SWF - Shockwave Flash File                                              |
