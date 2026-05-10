---
title: "Instalace Xorg a window manageru DWM"
date: 2022-02-05
author: "archos"
draft: false
categories: ['Návody']
tags: ['DWM']
---

Další díl seriálu o Arch Linuxu od[ Tondy Fischera](https://github.com/raven2cz). Tento 4. díl pojednává o instalaci Xorg a dynamického tiling window manageru DWM. Provede Vás postupně základní instalací v OS Arch Linux a seznámí se základním ovládáním prostředí. Ve finále budete mít systém nachystán pro svou běžnou práci a budete se moci pustit do studia systému 

# Instalace Xorg a vysvětlení .xinitrc

```
sudo pacman -S xorg xorg-xinit xterm
startx
```

Zobrazí se 3x xterms, vlevo je hlavní xterm. Pokud jej ukončíte zkratkou `ctrl+d`, dojde k ukončení celého xorg.

# [](https://github.com/raven2cz/tux/tree/main/210915-xorg-dwm-basic#instalace-a-kompilace-dwm-ručně)

# Instalace a kompilace DWM ručně

**DWM** má domov zde [https://suckless.org/](https://suckless.org/)

- Povídání o DWM na suckless stránkách [https://dwm.suckless.org/](https://dwm.suckless.org/)

- Velmi důležitý tutoriál k DWM [https://dwm.suckless.org/tutorial/](https://dwm.suckless.org/tutorial/)

- Arch wiki stránky [Arch Wiki DWM](https://wiki.archlinux.org/title/dwm)

- Seriál na root.cz [Suckless: dynamický správce oken dwm](https://www.root.cz/clanky/suckless-dynamicky-spravce-oken-dwm/) a [https://www.root.cz/serialy/suckless-project/](https://www.root.cz/serialy/suckless-project/)

## [](https://github.com/raven2cz/tux/tree/main/210915-xorg-dwm-basic#dwm-kompilace-a-instalace)

## DWM kompilace a instalace

```
sudo pacman -S git
mkdir -p ~/git/github
cd ~/git/github
git clone git://git.suckless.org/dwm
git clone git://git.suckless.org/st
git clone git://git.suckless.org/dmenu
cd dwm ## toto proved pro kazdy adresar dwm, st a dmenu
sudo make clean install ## postupne nainstalovat dwm, st, dmenu
```

## [](https://github.com/raven2cz/tux/tree/main/210915-xorg-dwm-basic#konfigurace-xinitrc-a-xresources)

## Konfigurace .xinitrc a Xresources

Zde již si připravíme .xinitrc komplexnější pro testy a spoštění WM (window managers) a DE (desktop environements) používaných v celém seriálu. Stažení provedeme z mých dofiles následujícím postupem.

```
cd ~/git/github
git clone https://github.com/raven2cz/dotfiles dotfiles-raven2cz
cd dotfiles-raven2cz
cp .xinitrc ~
cp .Xresources ~
nvim ~/.xinitrc ## zakomentovat setxkbmap -layout "us,cz" - prekryva hodne kl.zkratek s DWM!
```

## [](https://github.com/raven2cz/tux/tree/main/210915-xorg-dwm-basic#spuštění-dwm)

## Spuštění DWM

```
startx ~/.xinitrc dwm
```

# [](https://github.com/raven2cz/tux/tree/main/210915-xorg-dwm-basic#první-bash-script)

# První Bash Script

Ukázka prvního jednoduchého bash skriptu pro zobrazení hodin vpravo nahoře v `xsetroot` sekci.

```
nvim ~/.local/bin/dwm_time
#!/bin/bash
while true; do
   xsetroot -name "$( date +"%F %R" )"
   sleep 1m    # Update time every minute
done

chmod ug+x ~/.local/bin/dwm_time
```

Nutno přidat `$HOME/.local/bin` do `/etc/profile` Přidejte se sudo do tohoto souboru řádku: `appendpath '/home/box/.local/bin'= za ostatní již existující a soubor uložte. Nutný restart nebo zavolání z daného terminálu příkaz =source /etc/profile`.

# [](https://github.com/raven2cz/tux/tree/main/210915-xorg-dwm-basic#první-wallpaper)

# První Wallpaper

Provede alespoň základní nastavení pozadí, jsme suckless, víc zatím dělat nebudeme, záleží nám na efektivě a minimalismu. Stáhněte si své oblíbené obrázky pomocí firefox nebo přes `/mnt` sdílený adresář. Pro ostatní mohu nabídnout sbírku mých public wallpapers pro demonstraci.

```
cd ~/git/github
git clone https://github.com/raven2cz/public-wallpapers
```

Použijeme prohlížeč obrázků `feh` pro nastavení pozadí. [Arch-Wiki FEH](https://wiki.archlinux.org/title/feh#Set_the_wallpaper)

```
sudo pacman -S feh
feh --bg-scale ~/git/github/public-wallpapers/00007-minimal-forest.jpg
```

Později si ukážeme, jak tyto změny zahrnout do našeho `autorun` skriptu při spuštění DWM.

# [](https://github.com/raven2cz/tux/tree/main/210915-xorg-dwm-basic#dwm-flexipatch)

# DWM-Flexipatch

Zjednodušená možnost patches pro DWM pomocí flexipatch project.

- [https://github.com/bakkeby/dwm-flexipatch](https://github.com/bakkeby/dwm-flexipatch) Nutné provést git clone repository. Editovat soubor `config.def.h`. na hodnotu 1 nastavit patches, které chcete aktivovat, uložit soubor. Na závěř standardně zavolat `sudo make install`, zkompiluje dwm a umístí jej do spouštěcích adresářů.

https://www.youtube.com/watch?v=Z9grvRgriX4

# [](https://github.com/raven2cz/tux/tree/main/210915-xorg-dwm-basic#důležité-odkazy)

# Důležité odkazy

- [Youtube Channel TUX: Svět Linuxu](https://www.youtube.com/user/tondafischer/featured)

- [archlinux.org](https://archlinux.org/)

- [wiki.achlinux.org](https://wiki.archlinux.org/)

- [fishlive.org/blog](https://fishlive.org/en/blog-tech-art/arch)

- [github/raven2cz/tux](https://github.com/raven2cz/tux)

- [github/raven2cz/dotfiles](https://github.com/raven2cz/dotfiles)