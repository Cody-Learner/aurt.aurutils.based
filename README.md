## Aurt, AUR helper (aurutils based)
![1](https://user-images.githubusercontent.com/36802396/37560155-a1e0bdb6-29f0-11e8-827a-291d0def2176.png)
![22](https://user-images.githubusercontent.com/36802396/37556068-e7159b9c-29ad-11e8-8076-f85c9f31a067.png)
![44](https://user-images.githubusercontent.com/36802396/37574487-61aee490-2ade-11e8-9925-78ae4d651f4b.png)
![33](https://user-images.githubusercontent.com/36802396/37560287-b67d6d80-29f2-11e8-82c1-82e3cdd23845.png)

Aurt (new version based on aurutils) is an Arch Linux AUR helper bash script currently under development.

Aurt is intended to ease the transition into setting up and using aurutils. Aurutils brings AUR helpers to a whole new level with it's feature set and integration with pacman. Along with this comes more work to setup and use. Aurt is a small (~400 lines), very straight forward, easy to follow, edit, customize, etc  bash wrapper script, around aurutils, pacman, etc that ties all the various scripts into a common cli interfce with pacman like commands + some aurt specific, also has a cli command menu on the base interface.


Aurt and aurt-info are currently in alpha phase. The feature set is not yet 100% stable. The aurt script is accompanied by aurt-info script to provide user feedback when using aurt. Place both aurt and aurt-info scripts in $PATH for out of the box operation.

These scripts have been tested on my system managing around 100 AUR packages. All the rough edges I've have encountered so far have been worked out at this point.


For testing aurt and aurt-info, either set up per specs below or edit the script to your setup.

My setup for aurt:

Pacman local AUR repo: /var/cache/pacman/aur/

Pacman local AUR database files also in: /var/cache/pacman/aur/
```
$ pwd
/var/cache/pacman/aur

$ ls -l
aur.db.tar
aur.db -> aur.db.tar
aur.files.tar
aur.files -> aur.files.tar
```

I have the following set in the aurt script to change the default settings in aursync to use mc (midnight commander file manager) rather than vifm, and change the destination directory.

```
export PAGER=mc
export AURDEST=/home/cody/z-AUR-Aurt.git/
```



Pacman local AUR repo config file: /etc/aurt.conf

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


[aur]
SigLevel = Optional TrustAll
Server = file:///var/cache/pacman/aur


```


Pacman config. Just need to add the path to aurt.conf below the last official repo you have enabled per below.

```
#
# /etc/pacman.conf
#
# See the pacman.conf(5) manpage for option and repository directives

#
# GENERAL OPTIONS
#
[options]
# The following paths are commented out with their default values listed.
# If you wish to use different paths, uncomment and update the paths.
#RootDir     = /
#DBPath      = /var/lib/pacman/
CacheDir    = /var/cache/pacman/pkg/
#LogFile     = /var/log/pacman.log
#GPGDir      = /etc/pacman.d/gnupg/
#HookDir     = /etc/pacman.d/hooks/
HoldPkg     = pacman glibc
#XferCommand = /usr/bin/curl -C - -f %u > %o
#XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u
#CleanMethod = KeepInstalled
#UseDelta    = 0.7
Architecture = auto

# Pacman won't upgrade packages listed in IgnorePkg and members of IgnoreGroup
IgnorePkg   =
#IgnoreGroup =

NoUpgrade   =
#NoExtract   =

# Misc options
#UseSyslog
#Color
#TotalDownload
CheckSpace
#VerbosePkgLists

# By default, pacman accepts packages signed by keys that its local keyring
# trusts (see pacman-key and its man page), as well as unsigned packages.
SigLevel    = Required DatabaseOptional
LocalFileSigLevel = Optional
#RemoteFileSigLevel = Required

# NOTE: You must run `pacman-key --init` before first using pacman; the local
# keyring can then be populated with the keys of all official Arch Linux
# packagers with `pacman-key --populate archlinux`.

#
# REPOSITORIES
#   - can be defined here or included from another file
#   - pacman will search repositories in the order defined here
#   - local/custom mirrors can be added here or in separate files
#   - repositories listed first will take precedence when packages
#     have identical names, regardless of version number
#   - URLs will have $repo replaced by the name of the current repo
#   - URLs will have $arch replaced by the name of the architecture
#
# Repository entries are of the format:
#       [repo-name]
#       Server = ServerName
#       Include = IncludePath
#
# The header [repo-name] is crucial - it must be present and
# uncommented to enable the repo.
#

# The testing repositories are disabled by default. To enable, uncomment the
# repo name header and Include lines. You can add preferred servers immediately
# after the header, and they will be used before the default mirrors.

#[testing]
#Include = /etc/pacman.d/mirrorlist

[core]
Include = /etc/pacman.d/mirrorlist

[extra]
Include = /etc/pacman.d/mirrorlist

#[community-testing]
#Include = /etc/pacman.d/mirrorlist

[community]
Include = /etc/pacman.d/mirrorlist


# Path to aurt.conf
Include = /etc/aurt.conf

```

As soon as aurt and aurt-info become feature stable, I'll begin working on a generic configuration script to set up the basics required for aurutils usage. 

