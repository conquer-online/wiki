# DAT

A DAT file is generic data, some DAT files can be opened directly in a text-editor (such as Notepad), some need parsing a particular way and some are encrypted. This page lists the dat files in the client patch version and an overview of how to read these files. For an explanation of what these files do, see the individual file linked page.

## DAT File Formats Summary

* [**TQ File Cipher**](../../security/tq.md): Files which are marked as encrypted by TQ File Cipher can be decrypted & re-encrypted using [CPTSky File Manager](https://gitlab.com/conquer-online/tools/file-manager). The seed for each file is listed in brackets

* **RSA**: Files which are marked RSA have been encrypted by a TQ 2048-bit RSA private key. The public key is baked and obfuscated in the client binary. While it's possible to extract the public key from the binary to decrypt the file, it is not possible to re-encrypt without the private key.

* **SWF**: This dat file is actually a SWF file (Shockwave Flash). Rename the extension to SWF. [jpexs-decompiler](https://github.com/jindrapetrik/jpexs-decompiler) is a good & free decompiler for this file type.
 
* **Binary - Parsing Required**: The file is unencrypted, but has a binary structure. Opening it in Notepad may show hints of strings or more likely garbled text. A dedicated parser for the dat file is required to read it correctly. See the individual linked dat file for more information.

* **Unencrypted - Plain Text**: The file is unencrypted, you should be able to open the file in notepad without issues.

## Patch 5517

| File (relative to client root)                                  | DAT Format                                                              |
|-----------------------------------------------------------------|-------------------------------------------------------------------------|
| [./AutoPatch.dat](../content/autopatch.dat)                     | Unencrypted - Plain Text                                                |
| [./ini/UserHelpInfo.dat](../content/userhelpinfo.dat)           | TQ File Cipher (Seed: 2537)                                             |
| [./ini/Action.dat](../content/action.dat)                       | Binary - Parsing Required                                               |
| [./ini/Monster.dat](../content/monster.dat)                     | TQ File Cipher (Seed: 2537)                                             |
| [./ini/GameMap.dat](../content/gamemap.dat)                     | Binary - Parsing Required                                               |
| [./ini/AutoAllot.dat](../content/autoallot.dat)                 | Unknown & Unused                                                        |
| [./ini/MyAnimate.dat](../content/myanimate.dat)                 | RSA Encrypted                                                           |
| [./ini/LevelExp.dat](../content/levelexp.dat)                   | Unknown & Unused                                                        |
| [./ini/Shop.dat](../content/shop.dat)                           | RSA Encrypted                                                           |
| [./ini/Play.dat](../content/play.dat)                           | Custom Encrypted: Subtract 6 from each byte (Used in play.exe launcher) |
| [./ini/ShowHandTable.dat](../content/showhandtable.dat)         | RSA Encrypted                                                           |
| [./ini/suittype.dat](../content/suittype.dat)                   | RSA Encrypted                                                           |
| [./ini/RaceTrackProp.dat](../content/racetrackprop.dat)         | RSA Encrypted                                                           |
| [./ini/magictypeop.dat](../content/magictypeop.dat)             | TQ File Cipher (Seed: 2537)                                             |
| [./ini/slient.dat](../content/slient.dat)                       | TQ File Cipher (Seed: 2537)                                             |
| [./ini/mounttype.dat](../content/mounttype.dat)                 | TQ File Cipher (Seed: 2537)                                             |
| [./ini/levexp.dat](../content/levexp.dat)                       | TQ File Cipher (Seed: 1234)                                             |
| [./ini/tqist.dat](../content/tqist.dat)                         | Unknown (Referenced in ndist.dll)                                       |
| [./ini/UserHelpInfo.ini.dat](../content/userhelpinfo.ini.dat)   | TQ File Cipher (Seed: 2537)                                             |
| [./ini/MagicType.dat](../content/magictype.dat)                 | TQ File Cipher (Seed: 2537)                                             |
| [./ini/showhandlayout.dat](../content/showhandlayout.dat)       | RSA Encrypted                                                           |
| [./ini/itemtype.dat](../content/itemtype.dat)                   | TQ File Cipher (Seed: 2537)                                             |
| [./ini/MapDestination.dat](../content/mapdestination.dat)       | TQ File Cipher (Seed: 2537)                                             |
| [./ini/Tips.dat](../content/tips.dat)                           | Binary - Parsing Required                                               |
| [./version.dat](../content/version.dat)                         | Unencrypted - Plain Text                                                |
| [./res.dat](../content/res.dat)                                 | Unencrypted - Plain Text                                                |
| [./Server.dat](../content/server.dat)                           | RSA Encrypted                                                           |
| [./data/main/start.dat](../content/start.dat)                   | SWF - Shockwave Flash File                                              |
| [./data/main/role.dat](../content/role.dat)                     | SWF - Shockwave Flash File                                              |
| [./data/main/start-facebook.dat](../content/start-facebook.dat) | SWF - Shockwave Flash File                                              |
