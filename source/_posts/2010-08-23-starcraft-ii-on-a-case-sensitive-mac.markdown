---
layout: post
title: "StarCraft II on a Case Sensitive Mac"
date: 2010-08-23 22:37
comments: true
categories: 
---

* In Terminal, create the case insensitive installer Disc:

``` bash
    $ hdiutil create -size 8GB /starcraftdisc.sparsebundle -type SPARSEBUNDLE -fs HFS+J -volname "StarCraft II Disc" -layout NONE
    $ open /starcraftdisc.sparsebundle
```

* copy the contents of SC2-WingsOfLiberty-enUS-Installer downloaded with the starcraft downloader into "/Volumes/StarCraft II Disc"
It should have the following files:  
    * 102B Installer.app
    * 6.9G Installer Tome 1.MPQE
    * 40M Installer UI 2.MPQE
    * 2.4M Installer.exe
    * 8.3M Installer UI 1.MPQE
* Go to ~/Library search for blizzard and delete any blizzard preferences files
* Delete the Blizzard folder in /Users/Shared/
* In terminal create the destination for installation:

``` bash
    $ hdiutil create -size 8GB /insensitive.sparsebundle -type SPARSEBUNDLE -fs HFS+J -volname "insensitive" -layout NONE
    $ open /insensitive.sparsebundle
    $ mkdir /Volumes/insensitive/Applications/
    $ ln -s "/Volumes/insensitive/Applications/StarCraft II/" "/Applications/StarCraft II"
```

* start the installer
* select /Volumes/insensitive/Applications/StarCraft II/ as the installation directory