---
title: ArchBlocks - Installations-Framework für Arch Linux
date: 2012-10-09T12:32:00+0100
categories:
- Linux
- OSBN
tags:
- Archblock
- Arch
- Installation
slug: archblocks-installations-framework-fuer-arch-linux
---
Gestern bin ich auf ein interessantes Projekt gestoßen, mit dem man die Installation von Arch Linux automatisieren kann. [ArchBlocks](https://github.com/altercation/archblocks"ArchBlocks") besteht im Endeffekt aus einem Shellscript, das man nach dem Booten des Arch-Isos aufruft.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash">#!/bin/bash
# ------------------------------------------------------------------------
# archblocks - minimal, modular, manual Arch Linux install script
# ------------------------------------------------------------------------
# es@ethanschoonover.com @ethanschoonover http://github.com/altercation/archblocks
# INSTRUCTIONS -----------------------------------------------------------
# boot into Arch Install media and run (for this script only):
#
# curl https://raw.github.com/altercation/archblocks/master/sample_laptop.sh&quot; &gt; install.sh
# (...manually review the code! look at the blocks in the repo, then...)
# bash install.sh
# RESPOSITORY ------------------------------------------------------------ REMOTE=https://raw.github.com/altercation/archblocks/master
# CONFIG -----------------------------------------------------------------
HOSTNAME=tau
USERNAME=es
USERSHELL=/bin/bash
FONT=Lat2-Terminus16
FONT_MAP=8859-1_to_uni
LANGUAGE=en_US.UTF-8
KEYMAP=us
TIMEZONE=US/Pacific
MODULES=&quot;dm_mod dm_crypt aes_x86_64 ext2 ext4 vfat intel_agp drm i915&quot;
HOOKS=&quot;base udev autodetect pata scsi sata usb usbinput consolefont encrypt filesystems fsck&quot; #KERNEL_PARAMS=&quot;quiet&quot; # set/used in FILESYSTEM,INIT,BOOTLOADER blocks (this gets added to)
INSTALL_DRIVE=query # &quot;/dev/sda&quot; &quot;query&quot; or blank (blank is the same as &quot;query&quot;)

# as git, hg, svn and execute shell scripts automatically.
# list a url to use as a mr config file and archblocks core install will
# su to the new user&#039;s (USERNAME above) home and bootstrap using it.
# mr will be installed if this variable is set. # MR_BOOTSTRAP=https://raw.github.com/altercation/es-etc/master/vcs/.mrconfig
# BLOCKS -----------------------------------------------------------------
TIME=common/time_ntp_utc
FILESYSTEM=filesystem/gpt_luks_passphrase_ext4
BOOTLOADER=bootloader/efi_gummiboot
NETWORK=network/wired_wireless_default
#AUDIO=common/audio_alsa
#POWER=common/power_acpi
#XORG=xorg/xorg_wacom_fonts
#VIDEO=xorg/video_mesa_default
#DESKTOP=xorg/desktop_xmonad_minimal
#HARDWARE=hardware/laptop/lenovo_thinkpad_x220
#APPSETS=&quot;appsets/cli_hardcore appsets/vim_basics appsets/mutt_basics appsets/git_basics appsets/server_utils&quot;
# if you don&#039;t want to create a new block, you can specify extra packages from official repos or AUR here
PACKAGES=&quot;urxvt&quot;
AURPACKAGES=&quot;urxvi urxvtcd urxvtcd&quot;
# EXECUTE ----------------------------------------------------------------
. &lt;(curl -fsL &quot;${REMOTE}/blocks/_lib/helpers.sh&quot;); _loadblock &quot;_lib/core&quot;</code>
</pre>


In diesem Shellscript werden diverse Einstellungen wie Hostename, Benutzername, Timezone oder Module und Hooks eingetragen bzw. auf sogenannte Blocks verwiesen. Blocks sind im Grunde genommen wieder Shellscripts, welche sich auf einen bestimmten Bereich beziehen. Z. B. wie in folgendem Beispiel das Netzwerk.

<pre class="line-numbers" style="white-space:pre-wrap;">
<code class="language-bash"># ------------------------------------------------------------------------
# NETWORK # ------------------------------------------------------------------------
_installpkg netcfg
_installpkg coreutils
_installpkg dhcpcd
_installpkg iproute2
_installpkg bridge-utils # (optional) - for bridge connections
_installpkg dialog # (optional) - for the menu based profile and wifi selectors
_installpkg ifenslave # (optional) - for bond connections
_installpkg ifplugd # (optional) - for automatic wired connections through net-auto-wired
_installpkg wireless_tools # (optional) - for interface renaming through net-rename
_installpkg wpa_actiond # (optional) - for automatic wireless connections through net-auto-wireless _installpkg wpa_supplicant # (optional) - for wireless networking support

_daemon_remove network
_daemon_add net-auto-wireless net-auto-wired ifplugd net-profiles
mv /etc/wpa_supplicant/wpa_supplicant.conf /etc/wpa_supplicant/wpa_supplicant.conf.orig
echo -e &quot;ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=network\nupdate_config=1&quot; &gt; /etc/wpa_supplicant/wpa_supplicant.conf</code>
</pre>


Hier werden beispielsweise diverse Pakete installiert, die man für den Netzwerkbetrieb braucht. Danach werden Daemons entfernt bzw. hinzugefügt und die jeweilige Konfigurationsdatei kopiert und aktiviert. Auch wenn ich das ganze bisher noch nicht ausprobieren konnte, sieht es doch ziemlich interessant aus. Für Leute, die nur einen Rechner haben und diesen quasi nie neu aufsetzen mag das ganze wie mit Kanonen auf Spatzen schießen sein. Für alle andere ist es vermutlich eine gute Alternative zu Installation per Hand. Einen Support-Thread findet man im [Archlinux.org-Forum](https://bbs.archlinux.org/viewtopic.php?id=149597 "ArchBlocks Support-Thread").
