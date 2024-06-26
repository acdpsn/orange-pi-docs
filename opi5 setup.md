# My Orange Pi 5 Setup

This thing is a pain in the ass to set up so I'm writing down these notes in case I need to do this again.

Written for Armbian 24.5.1 Bookworm Minimal (Kernel: 6.1.43, Release date: Jun 21, 2024)

## Install image to ssd on Orange Pi 5

*Instruction taken from [Crosstalk Solutions](
https://www.crosstalksolutions.com/orange-pi-5-simple-overview-and-installation-with-m-2-ssd/)*

### Delete old OS

`sudo gdisk /dev/nvme0n1`

| command | function                     |
|---------|------------------------------|
| `p`     | show partition table         |
| `o`     | delete all partitions        |
| `w`     | write table to disk and exit |

### Extract image from xz

`unxz Armbian_24.2.1_Orangepi5_bookworm_legacy_5.10.160.img.xz`

### Flash image to ssd

`sudo dd bs=1M of=/dev/nvme0n1 status=progress if=Armbian_24.2.1_Orangepi5_bookworm_legacy_5.10.160.img`

---

## Disable root login and password login

**Copy your ssh keys to your server before doing this!**

`sudo nano /etc/ssh/sshd_config`

```bash
PermitRootLogin no
PasswordAuthentication no
PermitEmptyPasswords no
```

https://linux.die.net/man/5/sshd_config

## Change hostname

Set with armbian-config. This setting is in the Personal section.
