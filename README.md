vcromclaim
==========

Intro
-----
vcromclaim is a program to extract game ROMs from Wii Virtual Console games. 
It does this by analyzing an extracted Wii NAND filesystem, locating the ROMs, 
and extracting them.  It automatically detects and decompresses compressed ROMs.
It also extracts the game manual and save files for each Virtual Console game 
it encounters.

This is a fork of Bryan Cain's original version. This fork fixes a number of
bugs and adds compatibility with Famicom FDS, TurboGrafx CD, and some Neo Geo
games. 

Features
--------
* Extracts virtually all NES/Famicom/Disk System, SNES, PC Engine /
  TurboGrafx16 / TurboGrafx CD, Mega Drive/Genesis, Master System, and
  Nintendo 64 games without fail!
* Extracts several Neo Geo games: Magician Lord, King of the Monsters,
  Spinmaster, Neo Turf Master, Metal Slug, Metal Slug 2, Magical Drop 3, so that
  they are playable in MAME. Support for many other Neo Geo games can be added
  as long as the game is not encrypted.
* Can recreate a playable replica of the original ROM for SNES games where the 
  original sound data has been removed from the ROM, by re-encoding the PCM 
  sound data to BRR and restoring the BRR data to its original place in the ROM.
* Automatically extracts the built-in manuals in VC games.
* Automatically extracts saves for NES, SNES, Genesis, Nintendo 64 and Neo Geo
  games, converting them to the formats used by popular emulators for those
  platforms.
* Displays useful debugging information in the extraction process.
* Cross-platform - compatible with Linux, Windows, Mac OS X, and any other 
  platform supported by Python.

Requirements
------------
* [Python](http://python.org) 2.6 or 2.7 (or higher, but not Python 3.x)
* A NAND dump dumped by [BootMii](http://bootmii.org) and extracted by 
  [ShowMiiWads](http://code.google.com/p/showmiiwads) or [nandextract](http://github.com/Plombo/showmiiwads)

Usage
-----
The program is run by executing wiimetadata.py:  

    python wiimetadata.py nand_directory

Known Issues
------------
* NEO GEO: Because of the way Neo Geo games are made, part of the extraction
  process has to be hardcoded separately for each game. If your game is not
  supported, it might be trivial to expand neogeo_convert.py to include support
  for your game.
* NEO GEO: Many Neo Geo games are encrypted. At this time, there is no way of
  decrypting these games. (Though, in theory it should be possible. Worst case,
  one can extract the game as a Wad, run the game in Dolphin's debug mode, dump
  the RAM, and get the ROM data from there.)
* NEO GEO: The BIOS used for Neo Geo games (MVS verison for some, AES version
  for some) is extracted, but many of the support ROMS (e.g. 000-lo.lo,
  sfix.sfix, etc) are NOT extracted at this time.
* Extracted Famicom Disk System games are often modified for Virtual Console
  (such as the disk swapping screens being removed). For example, when the
  VC version of Bio Miracle Bokutte Upa is played in a "normal" emulator, it
  will display a flashing "Wait" screen when you are supposed to swap disk side.
* Some ROMs have been customized for the VC emulators, and are not playable or
  have issues in other emulators. This includes:
  * Bio Miracle Bokutte Upa (FDS) - instead of asking the player to swap disk,
    the game shows a flashing "Wait" screen.
  * Mario Tennis (N64) - 8 bytes are different in the middle of the file.
  * Ogre Battle (N64) - Bytes are different throughout the file.
* TURBOGRAFX CD: CD audio will play too slow in Mednefaren. Reencodeing the OGG
  files in 44kHz should make them run correctly.
* TURBOGRAFX CD: Super Air Zonk does not play.
* COMMODORE 64 and ARCADE: games cannot be extracted at this time.
* Save games for Sega Master System, Turbografx 16/CD, and Famicom Disk System
  are not extracted at this time.

Credits
-------
* [Bryan Cain](https://github.com/Plombo) - author of vcromclaim
* [hcs](http://hcs64.com) - author of C decompression code for Huf8, LZH8, and 
  romchu, all of which I (Bryan) ported to Python for vcromextract.
* [Hector Martin (marcan)](http://marcansoft.com/blog) - original author of the 
  Python LZ77 decompression code, which I heavily modified and expanded for 
  vcromextract.
* [Bregalad](http://www.romhacking.net/community/1067) - author of BRRTools, 
  a Java program on which the BRR encoder in vcromclaim was based.
* qwikrazor87 - author of PCE CD Tools, of which the TG CD data decompression
  was based.


