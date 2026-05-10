---
title: "Virtualbox Arch Linux nastavení"
date: 2022-01-16
author: "archos"
draft: false
categories: ['Návody']
tags: ['virtualbox']
series: ['Arch Linux instalace']
---

Další díl od [raven2cz](https://github.com/raven2cz)  pojednává o nastavení konzolového rozlišení a fontu. Dále pak nastavení Virtualbox Services pro dynamickou změnu rozlišení, sdílenou schránku a sdílení souborové složky. Doplňuje některé důležité body z minulého dílu. Po tomto díle budete mít Virtualbox Arch Image zcela připraven pro všechny ostatní další práce s Arch Linuxem.

# Nastavení TTY rozlišení a fontu

## [](https://github.com/raven2cz/tux/blob/main/210913-vbox-arch-nastaveni/vbox-arch-nastaveni.org#nastavení-rozlišení-pro-tty-framebuffer)

## Nastavení rozlišení pro TTY framebuffer

```
sudo nvim /etc/default/grub (zkontrolujte a změňte následující řádky)
GRUB_GFXMODE=1920x1080x32,auto
GRUB_GFXPAYLOAD_LINUX=keep

přegenerovat grub default do /boot/grub/grub.cfg příkazem z instalace:
sudo grub-mkconfig -o /boot/grub/grub.cfg
poweroff
(znovu spusťte virtualbox arch image)
```

Nyní máme již v pořádku nastaven framebuffer na fullhd, ale font je příliš malý (pokud máte velké rozlišení obrazovky).

## [](https://github.com/raven2cz/tux/blob/main/210913-vbox-arch-nastaveni/vbox-arch-nastaveni.org#nastavení-tty-fontu)

## Nastavení TTY fontu

```
sudo pacman -S terminus-font
setfont ter-132n  (změna je pouze dočasná, pro trvale zapsat do souboru)
sudo nvim /etc/vconsole.conf (zapište následující řádky)
FONT=ter-132n
FONT_MAP=8859-2
poweroff (reboot u vbox moc nefunguje)
```

# [](https://github.com/raven2cz/tux/blob/main/210913-vbox-arch-nastaveni/vbox-arch-nastaveni.org#virtualbox-guest-utils)

# Virtualbox Guest Utils

```
sudo pacman -S virtualbox-guest-utils
sudo systemctl status vboxservice.service
VBoxClient-all  (aktivovat všechny služby virtualboxu)
sudo systemctl restart vboxservice.service
sudo systemctl status vboxservice.service
poweroff
```

https://www.youtube.com/watch?v=LAN3lbgDWP4&t=209s

# Důležité odkazy

- [Youtube Channel TUX: Svět Linuxu](https://www.youtube.com/user/tondafischer/featured)

- [archlinux.org](https://archlinux.org/)

- [wiki.achlinux.org](https://wiki.archlinux.org/)

- [fishlive.org/blog](https://fishlive.org/en/blog-tech-art/arch)

- [github/raven2cz/tux](https://github.com/raven2cz/tux)

- [github/raven2cz/dotfiles](https://github.com/raven2cz/dotfiles)