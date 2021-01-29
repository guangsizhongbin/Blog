---
title: "Archlinux"
date: 2021-01-29T21:41:22+08:00
lastmod: 2021-01-29
author: "xiaonan"
math:
 enable: true

tags: [archlinux]
categories: [archlinux]
---


Arch Linux is an independently developed, x86_64-optimised Linux distribution targeted at competent Linux users.
<!--more-->

# Pre-installation

## download
### ios

[download](https://www.archlinux.org/download/)

### copy

1. sudo fdisk -l
2. dd bs=4M if=path/archlinux.iso of=/dev/sdx status=progress oflag=sync

### Partition the disks

1. fidsk -l
2. cfdisk xxx
3. format
	- Boot: mkfs.fat -F32 /dev/sdx_Boot
	- Root: mkfs.ext4 /dev/sdx_Root
4. mount
	- mount /dev/sdx_Root /mnt
	- mkdir /mnt/boot
	- mount /dev/sdx_Boot /mnt/boot

# Installation
## connect to the internet

1. iwctl
2. device list
3. station <wlan0> scan
4. station <wlan0> get-networks
5. station <wlan0> connect xxxx
6. quit

## Update the system clock

timedatectl set-ntp true

## Select the mirrors

vim /etc/pacman.d/mirrorlist

reflector --verbose --latest 5 --country China --sort rate --save /etc/pacman.d/mirrorlist

## Install essential packages

pacstrap /mnt base linux linux-firmware vim sudo

# configure the system
## Fstab

genfstab -L /mnt >> /mnt/etc/fstab

`-L` define by labels

## chroot

arch-chroot /mnt

## Time zone

1. Set the time zone
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

2. Run hwclock
hwclock --systohc
	
## Localization	

1. Uncomment `en_US.UTF-8 UTF-8` in `/etc/locale.gen` and generate it with `locale-gen`

2. Create the `/etc/locale.conf` file, and set the `LANG` variable accordingly:`LANG="en_US.UTF-8"`

## Network configuration

1. Create the hostname file in `/etc/hostname`

```
myhostname
```

2. Add matching entries to `/etc/hosts`

```
127.0.0.1	localhost
::1			localhost
127.0.1.1	myhostname.localdomain	myhostname
```

## Root password
passwd

## Boot loader

1. Install Boot loader packages

pacman -S os-prober ntfs-3g grub efibootmgr

2. grub-install

grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub

3. grub-mkconfig

grub-mkconfig -o /boot/grub/grub.cfg

## Intel-ucode

pacman -S intel-ucode


## Reboot

1. umount /mnt/boot
2. umount /mnt
3. reboot


# Post-installation
## KDE Plasma

1. install Xorg

sudo pacman -S xorg

2. KDE applications

sudo pacman -S plasma konsole dolphin

5. systemctl enable

sudo systemctl enable NetworkManager
sudo systemctl enable sddm

## Add a user to Wheel group

1. add User

useradd -m -G wheel -s /bin/bash xxx

2. `visudo`

uncomment `#`#%wheel ALL=(ALL)

3. passwd

passwd xxx


## Reboot

# software Installtion

## archlinxcn

1. vim `/etc/pacman.conf`

```
[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
Server = https://mirrors.cloud.tencent.com/archlinuxcn/$arch
Server = https://mirrors.zju.edu.cn/archlinuxcn/$arch
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
```
2. sudo pacman -S archlinuxcn-keyring

## git

1. download

sudo pacman -S git

2. config

```
git config --global user.name feng
git config --global user.email guangsizhongbin@gmail.com
```
3. SSH key

```
ssh-keygen -t rsa -C "guangsizhongbin@gmail.com"
```

4. test connect

ssh -T git@github.com

![](https://cdn.jsdelivr.net/gh/guangsizhongbin/picture/20200611192918.png)

4. upload id_ras.pub to github

![](https://cdn.jsdelivr.net/gh/guangsizhongbin/picture/20200611192435.png)




## yay

1. git clone https://aur.archlinux.org/yay.git
2. cd yay
3. sudo pacman -S base-devel
4. makepkg -si


## font

1. sudo pacman -S nerd-fonts-complete
2. sudo pacman -S wqy-zenhei wqy-bitmapfont wqy-microhei ttf-wps-fonts adobe-source-han-sans-cn-fonts adobe-source-han-serif-cn-fonts

## v2ray

sudo pacman -Sy v2ray

sudo pacman -Sy qv2ray
	
![](https://img.fengqigang.cn//img/20201109111828.png)

	
## joplin

yay joplin
	
## Obsidian

yay -S obsidaian
	

### support nvim

![](https://cdn.jsdelivr.net/gh/guangsizhongbin/picture/20200618_2115_1592486139.png)

##  anki

sudo pacman -S anki

### add-on

1. AwesomeTTS (Google Cloud Text-to-Speech) [unofficial] `814349176` 
2. Fast Word Query: Multi-threaded queries for words from local or web dictionaries `1807206748`
3. Image Occlusion Enhanced for Anki 2.1 (alpha) `1374772155`
4. ReviewHeatmap `723520343`
5. Browser: Table/Editor side-by-side `831846358`
6. Beautify Anki (Material design , Deck Background and icon ) `1150874988`
7. Batch Editing `291119185`
8. editor: apply font color, background color, custom class, custom style `1899278645`
9.Edit Field During Review `1020366288`

## GPU

sudo pacman -S linux-headers

sudo pacman -S nvidia bbswitch optimus-manager-qt-kde

systemctl enable optimus-manager.service


## kde connect

sudo pacman -S kdeconnect

##  screen-shot

1. yay flameshot (community)

- shortcuts(`flameshot gui`)

![](https://cdn.jsdelivr.net/gh/guangsizhongbin/picture/20200611_1855_1591872921.png)

2. sudo pacman -S peek

![](https://cdn.jsdelivr.net/gh/guangsizhongbin/picture/20200611190005.png)

- xclip
	sudo pacman -S xclip

![](https://img.fengqigang.cn//img/20200912184425.png)

## widget

- Network speed
- pager

##  music

sudo pacman -S iease-music


##  googlechrome

sudo pacman -S google-chrome

###  plugin

- Dark Reader
- 沙拉查词
- AdBlock
- Vimium
- infinity
- octotree
- language Tool
- SimpleExManage

##  video

sudo pacman -S mpv
sudo pacman -S vlc

##  neovim

sudo pacman -S neovim

- plugin
sudo pacman -S ctags

- clipboard
sudo pacman -S xclip

- node.js
sudo npm install -g neovim

- python
pip install neovim

- C/C++
sudo pacman -S ccls

## fcitx

1. download

sudo pacman -S fcitx fctix-im kcm-fcitx

2. vim `~/.xprofile`

```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```
3. sogou-input

```
	yay -Sy fcitx-sogoupinyin
```

	

## download

1. you-get

sudo pacman -S python-pip

sudo pip3 install you-get

2. youtube-dl

sudo pip3 install youtube-dl

### aria2 + youtube-dl

youtube-dl -f 22 https://www.youtube.com/playlist\?list\=PLFx-dS8yeeGPPQAdpV6hiAqgi4Qzohcmk --external-downloader aria2c --external-downloader-args "-x 16  -k 1M"

3. wget
sudo pacman -S wget

```
wget -c "www.baidu.com" -O baidu.index.html
```


4. aria2
sudo pacman -S aria2


## zsh

1. zsh
sudo pacman -S zsh

2. export https_proxy="https://0.0.0.0:8119"

3. oh-my-zsh
`export https_proxy="http://0.0.0.0:8189"`

`sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`


4. plugin

- zsh-autosuggestions
`git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions`



## bluetooth

sudo pacman -S  pulseaudio-alsa pulseaudio-bluetooth bluez bluez-libs bluez-utils

yay -S bluez-firmware

systemctl enable bluetooth

systemctl start bluetooth


## pdf

yay Okular


## Clion

sudo pacman -S clion clion-jre clion-cmake clion-gdb clion-lidb

## java

sudo pacman -S jdk

## compress/decompress

sudo pacman -S ark

## drawing

sudo pacman -S KolourPaint

## 图像查看

sudo pacman -S Gwenview

## downloader

	- motrix
yay -S aur/motrix

## WPS

sudo pacman -S wps-office-cn

yay -S wps-office-mui-zh-cn ttf-wps-fonts


## nutstore
	
sudo pacman -S nutstore

## timeout

sudo pacman -Syyu --disable-download-timeout


