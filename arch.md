# Installation
Create bootable USB stick, start up Arch Linux live environment

## Disk partitioning
* Find target disk (e.g. /dev/sda)
```bash
fdisk -l
```

* Start fdisk
```bash
fdisk /dev/sda
```

p - list all partitions
d - delete partition
n - new partition

* Create boot partition ( n, p, partition number 1, size: from 2048 to +200M )
* Create swap partition ( n, p, partition number 2, size )
* Create root partition ( n, p, partition number 3, size )
* Write changes to disk ( w )

Back to linux console

* Create file systems (boot and root)
```bash
mkfs.ext4 /dev/sda1
mkfs.ext4 /dev/sda3
```

* Create swap
```bash
mkswap /dev/sda2
swapon /dev/sda2
```

## Actual installation
* Mount root partition
```bash
mount /dev/sda3 /mnt
```

* Create boot directory, mount boot partition to it
```bash
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
```

* Install Arch Linux and any additional packages
```bash
pacstrap /mnt base base-devel linux linux-firmware vim htop
```

* Wait for it...

## Initial configuration

* Generate fstab (file with partitions to be mounted at system start)
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

* Jump into installed Arch Linux
```bash
arch-chroot /mnt
```

* Set up ntp
```bash
timedatectl set-ntp true
```

* Set up timezone
```bash
ln -sf /usr/share/zoneinfo/Europe/Moscow /etc/localtime
```

* Check time
```bash
date
```

* Set locale

Edit /etc/locale.gen, uncomment desired locales, generate them
```bash
vim /etc/locale.gen
locale-gen
echo "LANG=en-US.UTF-8" >> /etc/locale
```

* Install network manager
```bash
pacman -S networkmanager
systemctl enable NetworkManager
```

* Install GRUB
```bash
pacman -S grub
grub-install --target=i386-pc /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

## User management

* Set up root password
```bash
passwd
```

* Set up wheel group (administrator group)
```bash
EDITOR=vim visudo
```

Uncomment line "# %wheel ALL=(ALL) ALL"

* Add new user
```bash
useradd -m user
passwd user
```

* Add user to wheel group
```bash
usermod -aG wheel user
```

## Done

* Exit from arch-chroot and reboot
```bash
exit
reboot
```

# Desktop

* Log in as regular user

* Install video drivers (vm example) and xorg server
```bash
sudo pacman -S xf86-video-fbdev xorg xorg-xinit xterm
```

* Initialize x server
```bash
sudo xinit
```
