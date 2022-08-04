# search for a keybaord layout
localectl list-keymaps | grep RU

loadkeys <YOUR KBD layout>

# WIFI Set up
wifi-memu

# sync time
timedatectl set-ntp true

# Sync mirrors
pacman -Syyy
pacman -S reflector
reflector -c US -a 6 --sort rate --save /etc/pacman.d/mirrorlist
pacman -Syyy

# Format and mount partitions
fdisk /dev/xxx
boot - 200M
SWAP - 12GB
/ - 25G
HOME - REST

mkfs.ext4 /dev/sda1 for boot
mkfs.ext4 /dev/sda3 for /
mkfs.ext4 /dev/sda4 for /home

mkswap /dev/sda2 - for [SWAP]
swapon /dev/sda2

mount /dev/sda3 /mnt

mkdir /mnt/home
mount /dev/sda4 /mnt/home

mkdir /mnt/boot
mount /dev/sda1 /mnt/boot


# installing archlinux
pacstrap /mnt base linux linux-firmware vim base

# create a fstab file
genfstab -U /mnt >> /mnt/etc/fstab

# change root into new /mnt
arch-chroot /mnt

# set timezone
ln -sf /usr/share/zoneinfo/America/Boise /etc/localtime
hwclock --systohc --utc

# generate locale
# uncoment all us and ru locales from /etc/locale.gen
vim /etc/locale.gen
locale-gen
echo "LANG=en_US.UTF-8" >> /etc/locale.conf

# set hostname config
echo "archbook" >> /etc/hostname

# create a hosts file
vim /etc/hosts
127.0.0.1	localhost
::1	localhost
127.0.1.1	archbook.localdomain archbook

# set password
passwd

# install NetWork manager
pacman -S grub networkmanager base-devel linux-headers git vim reflector X11 xorg-server xorg-xinit nm-applet wpa_supplicant network-manager-applet wireless_tools webkit2gtk ttf-linux-libertine ttf-inconsolata

openssh


# Configure grub bootloader
grub-install --target=i386-pc /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg

# activate a couple of services
systemctl enable NetworkManager
systemctl enable sshd


# add a new user
useradd -mG wheel stan
passwd stan


# change sudo priveleges
EDITOR=vim visudo

## Here I give wheel users the ability to run core comands without asking for password
%wheel  ALL=(ALL) NOPASSWD: /usr/bin/shutdown,/usr/bin/reboot,/usr/bin/mount,/usr/bin/umount,/usr/bin/pacman -Syu,/usr/bin/packman -Syyu,/usr/bin/packer -Syyu,/usr/bin/systemctl restart NetworkManager,/usr/bin/rc-service NetworkManager restart, /usr/bin/pacman -Syyu --noconfirm

#This keeps you from needing to reinsert your password in each different terminal a wheel user uses sudo in
Defaults !tty_tickets


#exit from the installer
exit

# unmount all the partitions
umount -a

reboot


# WIFI connection
nmtui


umount -a

# additional information and installation
# Install yay
cd /opt
sudo git clone https://aur.archlinux.org/yay.git
sudo chown -R username:usergroup ./yay-git
cd yay-git
makepkg -si

# Configure Russian Keyboard
localectl --no-convert set-x11-keyboard us,ru pc105 "" grp:alt_space_toggle