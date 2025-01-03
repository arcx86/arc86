+++
date = '2024-03-14T15:58:00Z'
lastmod = '2024-03-15T19:57:00Z'
draft = false
title = 'Daily Driving Debian'
description = 'How I set up Debian 12 on my Dell Precision 5820 with Nvidia RTX 4060 graphics.'
tags = ['tech']
+++

I have fully switched from Windows 11 to Debian 12 on my Dell Precision 5820 and am now quite comfortable with keeping it as my daily driver, with no real need or urge to go back.

Originally, with the release of KDE Plasma 6, I was keen to give it a try on Arch, attempting to run it on my Nvidia RTX 4060 with Wayland. Unfortunately, I ran into a number of graphics/performance issues and general bugginess that Plasma unfortunately has a reputation for.
After spending some time troubleshooting and failing to find stable solutions, I was drawn to Debian + Xfce4 thanks to my [recent positive experiences with it]({{< ref "/blog/debian-thinkpad.md" >}}).

Using a new GPU like my RTX 4060 with this combination always seemed counter-intuitive due to Debian providing older packages by default; As of my writing this post, the Nvidia drivers on the stable channel are on version 525.147.05 dated 2023-10-31.
After testing it in various scenarios, I'm happy to say that so far it's been my best desktop Linux experience yet, so far with no real need to switch to the rolling release Testing or Unstable channels.

I installed Debian from the latest install CD ISO, partitioned my SSD with separate root and home partitions - no Swap partition as I prefer using a [Swap file](https://wiki.archlinux.org/title/swap#Swap_file).

The OS required a little configuration after the initial install, starting with proprietary Nvidia graphics drivers as per [Debian's documentation](https://wiki.debian.org/NvidiaGraphicsDrivers#Debian_12_.22Bookworm.22):

- Adding contrib & non-free repos to /etc/apt/sources.list
```bash
deb http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware

deb http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
deb-src http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware

# bookworm-updates, to get updates before a point release is made;
# see https://www.debian.org/doc/manuals/debian-reference/ch02.en.html#_updates_and_backports
deb http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware
```
- If 32-bit packages are required - such as [Steam](https://wiki.debian.org/Steam) - enable multiarch support with `sudo dpkg --add-architecture i386 && sudo apt update`
- Installing *nvidia-driver* & *firmware-misc-nonfree* packages and for 32-bit, *nvidia-driver-libs:i386*

A few additional changes were required to improve Nvidia stability and functionality:
- Added the following line to */etc/modprobe.d/nvidia-kernel-common.conf* in order to enable [DRM kernel mode](https://wiki.archlinux.org/title/NVIDIA#DRM_kernel_mode_setting) setting: `options nvidia-drm modeset=1` which then returns a value of Y after a reboot when running `sudo cat /sys/module/nvidia_drm/parameters/modeset`
- Preserving video memory after suspend/screen lock to improve the stability of hardware accelerated processes by uncommenting the `options nvidia-current NVreg_PreserveVideoMemoryAllocations=1` line in */etc/modprobe.d/nvidia-options.conf*
- Enabling the relevant systemd services:
`sudo systemctl enable nvidia-suspend.service`, `sudo systemctl enable nvidia-hibernate.service` & `sudo systemctl enable nvidia-resume.service`
- Discord no longer crashes when the PC wakes from sleep after these changes have been implemented and the PC rebooted.

Note that the proprietary Nvidia drivers/kernel modules are not SecureBoot signed, unlike the stock Debian install media/installation.
I personally have SecureBoot disabled, but Debian provides documentation on self-signing keys which is required for Nvidia users [here](https://wiki.debian.org/SecureBoot#MOK_-_Machine_Owner_Key).

I also wanted to switch to [PipeWire](https://wiki.debian.org/PipeWire) for my audio server, as in my experience it does a great job of wrangling the various Linux audio servers and services, keeping everything working together nicely.

- Installed *pipewire*, *wireplumber*, *pipewire-pulse* & *pipewire-alsa* packages
- Enabled WirePlumber systemd **user** service (without sudo) `systemctl --user --now enable wireplumber.service`
- My Fiio K5 Pro DAC/headphone amp supports higher bitrates which can be dynamically adjusted for audiophile listening with `pw-metadata -n settings 0 clock.force-rate 192000`

I set up bluetooth with the following steps.

- Installed *bluez* & *blueman* packages.
- Ensured the *bluetooth* systemd service was enabled.
- I use a TP-Link UB5A Bluetooth USB dongle which is plugged into my PC's internal USB port. It required the *firmware-realtek* package.

With this setup, I've been enjoying a stable & high-performance system with no issues I can find so far. Debian's wide selection of packages coupled with Flatpak (for a few edge cases such as Plex Player) has provided me with all the software I need and no headaches yet.

I'm keeping an eye on Nvidia Wayland compatibility on Arch as I still really want to try out Plasma 6 once it becomes more stable.
