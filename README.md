## Aurt, AUR helper (aurutils wrapper-script)

Aurt is an Arch Linux AUR helper, wrapper-script around aurutils.

Aurt is intended to ease the transition into setting up and using aurutils. Aurutils brings AUR helpers to a whole new level with it's feature set and integration with pacman. Along with this comes additional work to setup and use. Aurt is a small (~400 lines), very straight forward, easy to follow, edit, customize, etc wrapper script, around aurutils, pacman, etc that ties all the various scripts into a common cli interfce with pacman like commands + some aurt specific, also has a cli command menu on the base interface.


Aurt, aurt-info, and aurt-setup are currently in alpha phase. The feature set and or scripts are not stable. The aurt-setup script is ran once to automate the setup for aurutils. The aurt script is accompanied by and uses the aurt-info script to provide user feedback when using aurt. Place the scripts in $PATH for default, out of the box operation.

These scripts have been tested on my system managing around 100 AUR packages. All the rough edges I've encountered so far have been worked out at this point.

![aurt-ss1](https://user-images.githubusercontent.com/36802396/52738932-9f851b80-2f84-11e9-9247-d55733d6e87b.png)
Individual screenshots: https://cody-learner.github.io/
Combined: https://cody-learner.github.io/combined.html



## June 15 2021

I'm still using Aurt, although I stopped posting updates due to requiring an outdated version of aurutils as a dependency... <br>
I'll go ahead and say it. I'm kinda lazy and if it aint't broke, don't fix it?.                                              <br>
Been contemplating a complete rewrite of Aurt to drop aurutils and most other dependencies for a long time now.              <br>
Then pacman 6.0 comes along and breaks a feature aurt relied on in the obsolete version of aurutils.                         <br>
Two years should be enough time to procastinate, yes? So now I've began writing the new version of Aurt.                     <br>
It'll probably be a while till it's done enough to put up here though if continue the pattern. (some see them) lol           <br>
KC, I'll keep you posted and share the code as it progresses.                                                                <br>



## Oct 30 2019

Fixes for pacman 5.2 update.



## Feb 13 2019

This script ONLY works with aurutils version 1.5. It will not work with the current aurutils 2.0. <br>
For now, I'm staying on aurutils 1.5. until something else cause breakage of aurt. <br>
It's unlikely I'll rewrite aurt for aurutils 2.0 until it becomes unusable using aurutils 1.5.



## May 15 2018
To simplify testing without risking the health of or cluttering up your system, I've got the container image working pretty well at this point. Just git clone the repo: https://github.com/Cody-Learner/Arch-Image.git   If your Arch install is using systemd, follow the online guide: https://github.com/Cody-Learner/Arch-Image , start the container image and run the two on board scripts following the provided instructions. These scripts are necessary to keep the image compact enough to distribute here. <br>

Part of my motivation for building a test image is thinking that after trying it in a container, this will likely result in the users setting it up on their systems for regular use! My thoughts are aurt is too much a time saver and convenient to have just myself using it. But admittedly, this thinking may be influenced to a great extent because of my continued work on and use of it. <br>

Aurt may attract the user who is less experienced and see aurutils as intimidating or difficult, which admittedly created a delay in my trying it out, but who knows? It's also possible a highly skilled Linux user and or developer may just want something that comes close to fitting his preferences without having to be bothered with making a script. I know of at least one seemingly major player in the Arch ecosystem that seems to be using yaourt, and occasionally even somewhat defending it. If this true, I'm sure it fits his personal preferences or he'd just build his own. I'd hope any aurt users could and would easily modify any aspect of it to fit their preferences. <br>

With that said, would be cool to see an experienced script writer or programmer clone/copy this and share a cleaned up, sanitized version that could be considered "code elegance"* if it's possible. Or even see someone else take off with a fresh start of an aurutils wrapper written in shell. If I'm able to read and customize the code to suite my preferences, I just may switch to using it! <br>

*honestly still trying to figure out exactly what it is!
## April 29 2018 
Aurt-setup is now available. Screenshot: https://cody-learner.github.io/setup.html<br>
This script automates the setup required for running aurt and aurutils.<br>

To test run aurt:<br>
1) place all 3 scripts in somewhere in your $PATH.<br>
2) make the scripts executable, ie: chmod +x <script><br>
3) run aurt-setup as user (will prompt for password via sudo)<br>
4) run aurt as user<br>

Aurt-setup checks for dependencies, builds and/or installs them if needed, sets up a local aur repo in /var/cache/pacman/aur/, syncs the new aur repo, updates the system.<br>


## Setup an Arch systemd-nspawn container for testing aurt. (takes ~ 5 min)
Source: https://wiki.archlinux.org/index.php/Systemd-nspawn
```
1) Update system, install arch-install-scripts
$ sudo pacman -Syu
$ sudo pacman -S arch-install-scripts

2) Create container dir.
$ mkdir ~/Container/container1

3) Install Arch base, sudo, and git minus kernel, etc in container1
$ sudo pacstrap -i -c ~/Container/container1 base sudo git --ignore linux

4) When install is finished, switch to root and boot into the container:
$ su
# systemd-nspawn -b -D /home/$USER/Container/container1

5) Log in as root with no password

6) Set root password: 
# passwd

7) Setup user aurt:
# useradd -m -g users -G wheel,power,storage -s /bin/bash aurt

8) Set aurt password:
# passwd aurt

9) Setup sudo:
# EDITOR=nano visudo
Uncomment the following line and save edit:
# %wheel ALL=(ALL) ALL

10) Switch to user aurt and change to home dir:
$ su aurt
$ cd

11) Git clone the aurt repo:
$ git clone https://github.com/Cody-Learner/aurt.aurutils.based.git
$ mkdir bin
$ cp  -p aurt.aurutils.based/aurt* bin

12) Make scripts executable:
$ chmod +x bin/*

13) Set path to include ~/bin
$ export PATH=$PATH:$HOME/bin

14) Run aurt-setup:
$ aurt-setup

15) Run aurt for menu:
$ aurt
```
![88](https://user-images.githubusercontent.com/36802396/38223526-3c488eae-36a0-11e8-96db-8bdf152fc05b.png)
Reinstall cower and aurutils inside the container with aurt as a test and so they get registered in the local aur repo.<br>
Hit the [F10] key to escape midnight commander after reading, editing AUR package files.<br>

The container can be powered off by running poweroff from within the container.<br>
$ sudo poweroff

I copied my ~/Container contents to /var/lib/machines/ and created a custom tar'd container clone after working with systemd containers a bit.<br>

See 'man systemd-nspawn', 'man machinectl' and the Arch wiki link above for more info.

ENJOY!<br>
<br>
<br>
<br>

## Notes:

For testing aurt and aurt-info, either set up per specs below or edit the script to your setup.

My setup for aurt:

Pacman local AUR repo                  : /var/cache/pacman/aur/

Pacman local AUR database also setup in: /var/cache/pacman/aur/

The following should be present in /var/cache/pacman/aur after setup.
```
$ ls -go /var/cache/pacman/aur | awk '/aur[.db|.files]/ {print $7" "$8" "$9}'

aur.db -> aur.db.tar
aur.db.tar  
aur.files -> aur.files.tar
aur.files.tar
```

I have the following set in the aurt script to change the default settings in aursync to use mc (midnight commander file manager) rather than vifm, and change the destination directory.

```
export PAGER=mc
export AURDEST=/home/aurt/z-AUR-Aurt.git/
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

As soon as aurt and aurt-info become feature stable, I'll begin working on a generic configuration script to set up the basics required for aurutils usage.<br>
