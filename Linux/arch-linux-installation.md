# Arch Linux installation :



## steps :

### step 1 : sync time ( connect to the internet):
```
# write this later when you install again...

# to know the wifi devcie in your machine...

iwctl device list

# to connect to network ...
iwctl station {Device-name} connect {Network-Name} # it will prompt you for the password...

```

### step 2 : format the disk you want to install arch linux on and format it using fdisk.

* root should be not too big and not too small to hold your packages so around 75GiG
* boot can work with only 200MiB.(for legacy boot)
* swap can be X1.5 the amount of ram you have on your system.
* home can be the rest of the space since you're gonna be using it for everything


#### Note :

for the purposes of this guide root will be /dev/sda2 , home will be /dev/sda4 , swap will be /dev/sda3 , boot will be /dev/sda1

### step 3 : mount /mnt to the partition you want to be the root:

```
# for example:
mount /dev/sda2 /mnt
```
### step 4 :  create folders to mount /home and /boot on :
```
mkdir /mnt/home
mkdir /mnt/boot

```
### step 5 : mount /home , /boot to their respective folders:
```
## for example (mount home to home and boot to boot)
mount /dev/sda1 /mnt/boot
mount /dev/sda4 /mnt/home
```

### step 6 : create the file systems of all the partitoins:
```
mkfs.ext4 /dev/sda1
mkfs.ext4 /dev/sda2
mkfs.ext4 /dev/sda4
mkswap /dev/sda3

## remember to run the swap so it get's detected in later steps...
swapon /dev/sda3
```
### step 7 : start the pacstrap installer :
```
# in they recently removed the kernal and some of the systemd packages from the standard install so we have to install them here or in the future(the systemd package only in the future because it did some problems when i installed it early)
# i like to install the next packages...
pacstrap /mnt linux linux-firmware base-devel vim
```

### step 8 : setting up fstab (for the boot):
```
genfstab -U /mnt/etc >> /mnt//etc/fstab # we use the U option to get the physical address which is mor reliable.
```
## step 9 : change root into the new installed system:
```
arch-chroot /mnt
```
### Note :
now you are in the system and can start setting up you're options starting with the network manager and the bootloader (we will work with grub).

## step 10 : install network manager and grub and the systemd extra package :
```
pacman -S networkmanager grub systemd-sysvcompat
```
## step 11 : enable network manager :
```
systemctl enable NetworkManager

```

## step 12 : install and configure the grub bootloader :
```
# this is for legacy boot (please check online for the efi installation)
grub-install --target=i386-pc /dev/sda # you can ommit the target and grub will detect and set it for you (i only tried that on legacy boot)

# the configuration command for git...
grub-mkconfig -o /boot/grub/grub.cfg

```
## step 13 : setting up the locals :

open up the file locale.gen in any editor like vim and uncomment the languages that you wanna use with their iso lines.

```
# after you uncomment everything you wanna uncomment you use the next comand to generate the needed files...
locale-gen

```

## step 14 : create the locale.conf file :
create this folder in /etc/locale.conf

```
LANG=en-US.UTF-8 # look for another locale setting online if you want too
```


## step 15 : set up the time zone :

```
# we use the following command to create a link between the default zonetime that you're in and the one
ln -sf /usr/share/zoneinfo/path-to-your-zone /etc/localtime
```

## step 16 : set host name :


create a new folder in /etc/hostname and write your host name in it

## step 17 : set password for the root user :

```
passwd # this will prompt you to write the
```

## Final step 18 : exit from the change root and umount :

```
# to exit from the fake root environment...
exit

# to unmount everything and save all the changes you did in the fake root environment
umount -R /mnt

```
