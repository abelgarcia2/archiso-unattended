# Arch Linux Unattended Installation
Arch Linux ISO builder with a script for unattended installation.

## Build Your ISO
First, you need to clone this repository.
```
git clone https://github.com/abelgarcia2/archiso-unattended.git
```
Then, according to the [Arch Linux Wiki](https://wiki.archlinux.org/title/Archiso#Build_the_ISO),
you can build the ISO executing:
```
mkarchiso -v -w /tmp/archiso-unattended -o /path/to_out_dir /path/to/this_repo
```

> [!IMPORTANT]
> You need to install the [archiso](https://archlinux.org/packages/?name=archiso) package beforehand

## Download the ISO
Alternatively you can download the latest ISO version from
[this repo releases page](https://github.com/abelgarcia2/archiso-unattended/releases)

## Install the system
Once you have the ISO, you need to prepare an installation medium by following the instructions in
["Prepare an installation medium"](https://wiki.archlinux.org/title/Installation_guide#Prepare_an_installation_medium).
After that you can boot the live environment and run the `unattended-install`
script with the command:
```
unattended-install /path/to/installation_disk
```
This will install Arch Linux on ext4 partitions, with the [default configuration](#default-configuration).

## LVM Installation
You can use this script to install Arch Linux over LVM volumes instead of ext4 partitions.
To do this use the `--installation_type lvm` parameter. For example:
```
unattended-install /dev/sda --installation_type lvm
```

## LVM Encrypted Installation
You can use this script to install Arch Linux on LUKS encrypted partition with
LVM volumes inside. To do this use the `--installation_type lvm_encrypted` parameter and provide
an encryption key with `--encryption_key yourkey`. For example: 
```
unattended-install /dev/sda --installation_type lvm_encrypted --encryption_key secret
```

## LVM Encrypted With Detached LUKS Header And Encrypted /boot Installation
You can use this script to install Arch Linux on a LUKS-encrypted partition with
a separate LUKS header and an encrypted /boot stored on another disk. To do this use the
`--installation_type lvm_detached` parameter along with `--encryption_key yourkey` and
`--usb device`. For example:

```
unattended-install /dev/sda \
    --installation_type lvm_detached \
    --encryption_key secret \
    --usb /dev/sdb
```

## Default Configuration
- Timezone: UTC
- Root Password: arch
- Hostname: arch
- Swap Partition Size: RAM size
- Boot Partition Size: 1G
- Root Partition Size: 50G
- Home Partition Size: remaining free space
- Reboot machine after install: no

## Options
- `-t, --installation_type`: Set the installation type (ext4, lvm, lvm_encrypted, lvm_detached) (default: ext4)
- `-e, --encryption_key`: Set the encryption key for LUKS2 encrypted device
- `-p, --root_passwd`: Set the root password (default: arch)
- `--timezone`: Set the system timezone (default: UTC)
- `--host, --hostname`: Set the system hostname (default: arch)
- `--reboot`: Reboot machine after install
- `--swap`: Set the swap size, pass '-' to disable swap (default: RAM size)
- `--boot`: Set the boot partition size (default: 1G)
- `--root`: Set the root partition size (default: 50G)
- `--home`: Set the home partition size, pass - to use all free space (default: all free space)
- `--usb`: Set the usb drive to save encrypted /boot and detached LUKS header (only useful in lvm_detached installation)"
