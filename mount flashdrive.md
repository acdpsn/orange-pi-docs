# Mount a flashdrive to your debian server

### 1. List drives

`sudo fdisk -l`

output:

```
Device     Boot Start      End  Sectors  Size Id Type
/dev/sda1        8192 16099327 16091136  7.7G  c W95 FAT32 (LBA)
```

I have an 8gb flashdrive attached, so I look at drive sizes to find the device name.

### 2. Make mounting point

`sudo mkdir /media/usb`

### 3. Mount drive

`sudo mount /dev/sda1 /media/usb`

### 4. When you want to eject the flashdrive, unmount the drive

`sudo umount /media/usb`
