# aurt.aurutils.based
Aurt (this new version based on aurutils) is an Arch Linux AUR helper bash script currently under development.

Aurt is intended to ease the transition into setting up and using aurutils. Aurutils brings AUR helpers to a whole new level with it's feature set and integration with pacman. Along with this comes more work to setup and use. Aurt is a small (~400 lines), very straight forward, easy to follow, edit, customize, etc  bash wrapper script, around aurutils, pacman, etc that ties all the various scripts into a common cli interfce with pacman like commands + some aurt specific, also has a cli command menu on the base interface.


Aurt and aurt-info are currently in alpha phase. The feature set is not yet 100% stable. The aurt script is accompanied by aurt-info script to provide user feedback when using aurt. Place both aurt and aurt-help scripts in $PATH for out of the box operation. 
These scripts have been tested on my system managing around 100 AUR packages. All the rough edges I have encountered have been worked out at this point.


For testing aurt and aurt-help, either set up per specs below or edit the script to your setup.

My setup for aurt:

Local pacman AUR repo: /var/cache/pacman/aur/

Local pacman AUR database files also in: /var/cache/pacman/aur/

$ ls -l
aur.db.tar
aur.db -> aur.db.tar
aur.files.tar
aur.files -> aur.files.tar

Local pacman AUR repo config file: /etc/aurt.conf
```
#
# /etc/aurt.conf
#
#
# [default options]
# The following paths are commented out with their default values listed.
# If you wish to use different paths, uncomment and update the paths.
# RootDir     = /
# DBPath      = /var/lib/pacman/
# CacheDir    = /var/cache/pacman/pkg/
# LogFile     = /var/log/pacman.log
# GPGDir      = /etc/pacman.d/gnupg/
# HookDir     = /etc/pacman.d/hooks/
# HoldPkg     = pacman glibc
# XferCommand = /usr/bin/curl -C - -f %u > %o
# XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u
# CleanMethod = KeepInstalled
# UseDelta    = 0.7

# Put custom config options below this line.

[options]
CacheDir    = /var/cache/pacman/aur
CleanMethod = KeepInstalled
