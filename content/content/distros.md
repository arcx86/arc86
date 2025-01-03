+++
date = '2024-11-19T10:36:45Z'
lastmod = '2024-12-20T16:46:48Z'
draft = false
title = 'Linux Distros'
description = 'Recommended & useful Linux Distros'
weight = 5
+++

A breakdown of all Linux distros I have experience with or opinions on.

## APT-Based

### Debian

[Website](https://www.debian.org/) | [Packages](https://www.debian.org/distrib/packages)

The original APT-based distro all others are derived from.

Referred to as the "Universal Operating System" and can certainly find a place in most applications, but the slow release cycle with frozen package feature updates for ~2 years might not be suitable for desktop daily driving.

Great for servers or computers you only use sporadically with ([usually](https://github.com/keepassxreboot/keepassxc/issues/10725)) sane packaging defaults and only having to care about upgrading once every few years.

### Ubuntu

[Website](https://ubuntu.com/) | [Packages](https://packages.ubuntu.com/) | [Snap Packages](https://snapcraft.io/store)

The first distro to really see some mainstream adoption, helped to popularise the Linux desktop. Ubuntu used to be seen as the "default" distro recommended to beginners.

Pushes the Snap packaging standard very heavily to the point of no longer offering basic packages such as Firefox in the APT repos. Makes for a slower and arguably confusing experience for newcomers. Verges on being a walled garden with Snap not being used/supported on most other distros.

### Linux Mint

[Website](https://linuxmint.com/) | [Packages](https://packages.linuxmint.com/)

Ubuntu/Debian downstream distro advertised as being beginner friendly out of the box. Serves as a less corporate Ubuntu alternative with a more traditional desktop.

### Pop!_OS

[Website](https://pop.system76.com/)

Another Ubuntu derivative, this time vanilla GNOME-based. The team behind it have recently been working on the new [COSMIC desktop](https://system76.com/cosmic/) aiming to bring together Wayland and tiling window management under a more fully featured desktop environment.

---

## RPM-Based

### Fedora

[Website](https://fedoraproject.org/) | [Packages](https://packages.fedoraproject.org/s) | [RPM Fusion Packages](https://rpmfusion.org/)

Red Hat/IBM's testbed for Red Hat Enterprise Linux.

Offers a mostly stock GNOME/KDE desktop, rapidly adopts cutting edge features and frequently updates.

Uses the RPM package manager with DNF which I would argue is superior to APT. Only offers Free Software packages by default with [RPM Fusion](https://rpmfusion.org/) being strongly recommended for desktop users to access a greater selection of software as well as GPU drivers/codecs.

Great all around distro, recommended for new & experienced users alike, less suitable for niche non-standard setups than some other options.

### OpenSUSE

[Website](https://www.opensuse.org/) | [Packages](https://software.opensuse.org/)

An RPM-based distro separate from the Red Hat ecosystem, with its own corporate backer, SUSE. Offers a point as well as rolling release version. 

Comes preconfigured with some unusual defaults which may take some getting used to and can be reconfigured with the [YaST](https://yast.opensuse.org/) configuration tool. Features some great features such as Snapper for automatic system snapshots & easy rollbacks.

Codecs and some other non-free license software may require installation [using OPI from Packman repos](https://en.opensuse.org/SDB:Installing_codecs_from_Packman_repositories).

---

## Independent

### Arch

[Website](https://archlinux.org/) | [Packages](https://archlinux.org/packages/) | [AUR Packages](https://aur.archlinux.org/)

My desktop distro of choice for many years - In my opinion, offers one of the most "default" Linux experiences. Rolling release, bleeding edge, rapidly updated. 

Packages an excellent software selection (especially when paired with the [Arch User Repository](https://aur.archlinux.org/)) close to the original upstream, does not push any defaults on the user but requires making educated choices when configuring an installation from the ground up. 

Recommended for experienced Linux users or those with plenty of free time to learn.

### Void

[Website](https://voidlinux.org/) | [Packages](https://voidlinux.org/packages/)

Independent rolling release distro without systemd. 

Slower to release new packages than Arch, aiming for stability rather than bleeding edge. Developed by a small team for general use.

### Gentoo

[Website](https://www.gentoo.org/) | [Packages](https://packages.gentoo.org/)

Source-based distro requiring all packages to be compiled from source rather than offering binaries (with some exceptions for cowards).

Offers by far the most choice when installing, allowing a custom kernel to be built, supporting multiple init systems etc.

Only for those who know what they're doing and/or have a specific use case for building their own packages.

### Slackware

[Website](http://www.slackware.com/)

Oldest disto still seeing updated. Continues to follow much older design principles, feels closer to a true UNIX OS than most modern distros. 

Comes preinstalled with a large selection of packages & libraries, installing additional software is more difficult than on modern distros due to a lack of dependency resolution. 

Not recommended for most users.