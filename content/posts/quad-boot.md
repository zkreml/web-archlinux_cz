---
title: "Quad Boot"
date: 2022-02-11
author: "archos"
draft: false
categories: ['Návody']
tags: ['Grub2']
series: ['Arch Linux instalace']
---

Další díl seriálu  o [instalaci a nastavení Arch Linuxu](https://arch-linux.cz/series/arch-linux-instalace/) od [Tondy Fishera](https://github.com/raven2cz/tux), obsahuje plné nastavení reálného desktopu se čtyřmi operačními systémy s výběrovým dialogem pro zvolení, který systém si při spuštění počítače vybrat. Jedná se tedy o quad booting (dual booting je pouze pro dva operační systémy). Video je již i na našem[ PeerTube kanále.](https://peertube.arch-linux.cz/w/b3ajczWRf3XFy4vhCTPQz1)

# Diskový správce Gnome-Disks

```
sudo pacman -S gnome-disk-utility
```

- Moutovat diskové oddíly pomocí ikony ozubených kol, zvolit **Edit Mount Options**.

- Nastavit `Display Name` a `Mount Point` `/mnt/displayName`.

- Ověřit, že změny se správně zapsaly do `/etc/fstab`.

# [](https://github.com/raven2cz/tux/tree/main/210916-quad-boot#polkit-gnome)

# Polkit-Gnome

```
sudo pacman -S polkit-gnome
```

Spustit jej v `autorun.sh` skriptu.

# [](https://github.com/raven2cz/tux/tree/main/210916-quad-boot#support-ntfs-windows)

# Support NTFS (Windows)

```
sudo pacman -S ntfs-3g
```

Podpora NTFS a mountování win partitions.

# [](https://github.com/raven2cz/tux/tree/main/210916-quad-boot#grub-editace)

# Grub Editace

```
sudo nvim /etc/default/grub
# V Grub přidat parameter GRUB_DISABLE_OS_PROBER=false
sudo grub-mkconfig -o /etc/grub/grub.cfg

sudo pacman -S grub-customizer
```

# [](https://github.com/raven2cz/tux/tree/main/210916-quad-boot#grub-rozlišení-a-themes)

# Grub rozlišení a themes

## [](https://github.com/raven2cz/tux/tree/main/210916-quad-boot#konfigurace-vhodného-rozlišení)

## Konfigurace vhodného rozlišení

- restart, v grub tabulce stisk `C`, cmd grub line napsat `videoinfo`, opsat si nejlepší rozlišení, např. `2048x1080x32`.

- Edit opět stejně grub soubor v `/etc/default/grub`, nastavit v `GRUB_GFXMODE=2048x1080x32,auto` vaše rozlišení, ne moje. A nezapomenout přegenerovat grub přes `grub-mkconfig`!

## [](https://github.com/raven2cz/tux/tree/main/210916-quad-boot#instalace-grub2-themes)

## Instalace Grub2 Themes

```
cd ~/git/github
git clone https://github.com/vinceliuice/grub2-themes.git
sudo ./install.sh -t vimix -s 2k
```

https://www.youtube.com/watch?v=wj06-4Y7Pkk

# [](https://github.com/raven2cz/tux/tree/main/210916-quad-boot#důležité-odkazy)

# Důležité odkazy

- [Youtube Channel ](https://www.youtube.com/user/tondafischer/featured)[TUX](https://www.youtube.com/user/tondafischer/featured)[: Svět Linuxu](https://www.youtube.com/user/tondafischer/featured)

- [archlinux](https://archlinux.org/)[.org](https://archlinux.org/)

- [wiki.achlinux.org](https://wiki.archlinux.org/)

- [fishlive.](https://fishlive.org/en/blog-tech-art/arch)[org](https://fishlive.org/en/blog-tech-art/arch)[/blog](https://fishlive.org/en/blog-tech-art/arch)

- [github/raven2cz/tux](https://github.com/raven2cz/tux)

- [github/raven2cz/dotfiles](https://github.com/raven2cz/dotfiles)