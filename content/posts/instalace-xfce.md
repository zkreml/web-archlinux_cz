---
title: "Instalace Xfce"
date: 2022-03-18
author: "archos"
draft: false
categories: ['Návody']
tags: ['Xfce']
---

V osmém díle seriálu o instalaci [Arch Linuxu ](https://arch-linux.cz/series/arch-linux-instalace/) od [Tondy Fischera](https://github.com/raven2cz) se podíváme, jak instalovat a nastavit desktopové prostředí [Xfce](https://wiki.archlinux.org/title/Xfce_(%C4%8Ce%C5%A1tina)).

# XFCE

## [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#co-je-xfce)

## Co je XFCE?

[Xfce](https://wiki.archlinux.org/title/Xfce_(%C4%8Ce%C5%A1tina)) je lehké a modulární desktopové prostředí, které je v současné době založeno na GTK 3. Pro zajištění úplného uživatelského komfortu obsahuje správce oken, správce souborů, plochu a panely. Xfce lze jednoduše rozšiřovat pomocí extra pluginů.

## [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#dokumentace)

## Dokumentace

- [https://docs.xfce.org/](https://docs.xfce.org/)

- [https://www.xfce.org/](https://www.xfce.org/)

- [https://gitlab.xfce.org](https://gitlab.xfce.org)

- [Arch-Wiki:Xfce(čeština)](https://wiki.archlinux.org/title/Xfce_(%C4%8Ce%C5%A1tina))

## [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#moje-xfce-konfigurace)

## Moje Xfce Konfigurace

Toto repo samozřejmě nemůže obsahovat veškeré nutné části, protože se jedná o DE, které by vyžadovalo spíše distro. Bylo by nutné použít několik konfiguračních adresářů a zdrojových témat. Nicméně kompletní základní xfce konfigurace je systematicky oddělena a uložena ve formátu XML, který zde přikládám s MIT licencí.

- [https://github.com/raven2cz/xfce-config](https://github.com/raven2cz/xfce-config)

# [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#základní-instalace)

# Základní Instalace

Vše jsou meta balíky. Doporučuji nainstalovat celou tuto základnu meta balíků. Oproti jiným full DE, je toto pořád silně lightweight.

```
sudo pacman -S xfce4 xfce4-goodies

nvim ~/.xinitrc
# Overit umisteni radky
exec startxfce4
```

# [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#xfce4-settings-manager)

# Xfce4 Settings Manager

Spusťe z terminálu

```
xfce4-settings-manager
```

https://www.youtube.com/watch?v=tehEIbcYn8U

# [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#volba-sound-systemu)

# Volba Sound Systemu

Zvuk je velký topic. Stejně jako grafické karty na linuxu. Toto je pouze minimální zmínka o této problematice.

- [https://wiki.archlinux.org/title/Advanced_Linux_Sound_Architecture](https://wiki.archlinux.org/title/Advanced_Linux_Sound_Architecture)

- [https://wiki.archlinux.org/title/PulseAudio](https://wiki.archlinux.org/title/PulseAudio)

- [https://wiki.archlinux.org/title/PipeWire](https://wiki.archlinux.org/title/PipeWire)

Doinstalovat uřčitě při `pulseaudio` ještě `pavucontrol`, `alsa-utils`. `alsamixer`. [PipeWire](https://wiki.archlinux.org/title/PipeWire) je separátní topic a bylo by vhodné oddělené video, pokud bude zájem.

# [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#graphical-drivers-a-picom-aktivace)

# Graphical Drivers a Picom aktivace

Grafické drivers byly instalovány při základní instalaci, odkazuji tak na video [základní instalace systému](https://youtu.be/gpIFaCIB9Cg). Nyní je potřeba nahradit defaultní kompozitor naším picom nastaveným dle zlaté střední cesty z minulého dílu.

- Window Manager Tweaks > Compositor > Deaktivujte `Enable display compositing`

- Session and Startup > Application Autostart > + > přidejte name: `picom` command: `picom --experimental-backends --config $HOME/.config/picom/picom.conf`

Picom bude spuštěn v autostart xfce po novém spuštění xfce.

# [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#instalace-terminal-emulator-gpu-support)

# Instalace Terminal Emulator (GPU Support)

Doporučuji tyto terminal emulatory. V mém případě používám oba, aby se nehádaly.

```
sudo pacman -S kitty
sudo pacman -S alacritty
```

O terminálech si více povíme jindy. Nyní alespoň základní instalace a umět je spustit a používat v základní vanilla podobě.

# [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#přidání-whisker-menu)

# Přidání Whisker Menu

Whisker menu je základní Xfce kvalitní menu a spouštěč aplikací. Přidání extra pluginu do Panel1 instance na první místo v Items.

# [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#klávesové-zkratky-buď-linux-pro)

# Klávesové zkratky, buď Linux Pro

Vytvoř klávosvé zkratky používané v profi window managers, jako je dwm, xmonad, awesome, qtile, i3, bspwm.

- [Klávesové zkratky Xfce ArchWiki](https://wiki.archlinux.org/title/Xfce_(%C4%8Ce%C5%A1tina)#Kl%C3%A1vesov%C3%A9_zkratky)

## [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#klávesové-zkratky-pro-ovládání-hlasitosti)

## Klávesové zkratky pro ovládání hlasitosti

[https://wiki.archlinux.org/title/PulseAudio#Keyboard_volume_control](https://wiki.archlinux.org/title/PulseAudio#Keyboard_volume_control)

![](https://arch-linux.cz/wp-content/uploads/2022/03/xfce-effective-keybindings-619x1024.png)* Klávesové zkratky*

# [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#xfce-ricing---dracula-ricing)

# XFCE Ricing - Dracula Ricing

## Co je Ricing?

[https://jie-fang.github.io/blog/basics-of-ricing](https://jie-fang.github.io/blog/basics-of-ricing)

## [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#co-je-dracula-a-draculapro)

https://www.youtube.com/watch?v=VspS7Q9Spjs

## Co je Dracula a DraculaPro?

- [https://draculatheme.com/](https://draculatheme.com/)

- [https://draculatheme.com/pro](https://draculatheme.com/pro) ($49)

[![](https://github.com/raven2cz/tux/raw/main/211012-xfce-instalace/images/dracula-color-palette.png)](https://github.com/raven2cz/tux/blob/main/211012-xfce-instalace/images/dracula-color-palette.png)

## [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#aplikace-základních-themes-a-color-schemes)

## Aplikace základních themes a color schemes

- Postupujte podle pokynů na dracula stánkách pro jednotlivé aplikace a GTK3.

- Přejděte na záložku GTK na webu, nainstalujte `gtk-master.zip`

- Použijte z mých dotfiles konfigurace pro `kitty` a `alacritty`. obsahují dracula pro kitty a postelové barvy pro alacritty

- Nainstalujte a použijte fonty dle videa: `paru -S tty-droid tty-play`

- Aplikujte theme pro Midnight Commander z webu `dracula256.ini`

- Použijte zlatou střední cestu pro picom z dotfiles.

## [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#icons-a-mouse-cursors)

## Icons a Mouse Cursors

- `sudo paru -S papirus-icon-theme`

- `sudo paru -S numix-cursor-theme xcursor-comix-opaque xcursor-comix`

## [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#změna-základního-panel1)

## Změna základního Panel1

- Použijte mojí konfiguraci panelu, nebo manuálně nastavte komponenty dle videa

- Aplikujte/zkopírujte `gtk.css` styling do vašeho `~/.config/gtk-3.0`

- Alternativně můžete použít polybar (pozor je to výhoda i nevýhoda), viz můj projekt [Polybar-config](https://github.com/raven2cz/polybar-config)

## [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#public-wallpapers)

## Public-Wallpapers

- Stáhněte si moje public wallpapers [public-wallpapers](https://github.com/raven2cz/public-wallpapers)

- Link public-wallpapers přes `mkdir ~/Pictures/wallpapers && ln -s ~/git/github/public-wallpapers ~/Pictures/wallpapers/`

## [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#qt-a-gtk-jednotný-vzhled-aplikací)

## Qt a Gtk jednotný vzhled aplikací

- pročíst [Uniform look for Qt and GTK applications](https://wiki.archlinux.org/title/Uniform_look_for_Qt_and_GTK_applications)

- Gtk již máme zařízeno, neboť xfce staví na gtk-3.0 a s dracula theme jsme toto pořešili pro gnome aplikace automaticky

- Pro Qt aplikace nutno pořešit

Nainstalujte `sudo pacman -S kvantum-qt5`

- Checkout git repozitář `cd ~/git/github && git clone https://github.com/dracula/gtk.git`

- Spustit Kvantum Manager, nainstalovat Dracula (dle svého vkusu)

- Aplikovat v aplikaci Dracula jako aktvní téma

- Zkontrolovat si svůj `~/.xinitrc` nastavení `export QT_STYLE_OVERRIDE=kvantum`

## [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#doplňková-rožšíření)

## Doplňková rožšíření

- Aplikace pro nastavení osobních uživatelských detailů `sudo pacman -S mugshot`

- Editor nabídek pro Gnome s podporou XFCE `sudo pacman -S alacarte`

- Odstranění ikon na ploše `xfconf-query -c xfce4-desktop -v --create -p /desktop-icons/style -t int -s 0` (obnova nastavit 2)

- Nastavení zvukového motivu Smooth

Nainstalujte `libcanberra` pro PulseAudio

- Zahrnout `canerra-gtk-module` do proměnné prostředí `GTK_MODULES`

- V `Settings Manager > Appearance > Settings` nastavit =”Enable event sounds”=

- Nainstalujte z AUR `paru -S sound-theme-smooth`

- V Editoru nastavení (`xfce4-settings-editor`) nastavte v `xsettings/Net/SoundThemeName` na `Smooth` (pozor na velké písmeno)

- Zapněte a zvyšte hlasitost u `System Sounds` v mixéru zvuku, např. `pavucontrol`.

# [](https://github.com/raven2cz/tux/tree/main/211012-xfce-instalace#důležité-odkazy)

# Důležité odkazy

- [arch wiki:Xfce](https://wiki.archlinux.org/title/Xfce_(%C4%8Ce%C5%A1tina))

- [Youtube Channel TUX: Svět Linuxu](https://www.youtube.com/user/tondafischer/featured)

- [archlinux.org](https://archlinux.org/)

- [wiki.achlinux.org](https://wiki.archlinux.org/)

- [fishlive.org/blog](https://fishlive.org/en/blog-tech-art/arch)

- [github/raven2cz/tux](https://github.com/raven2cz/tux)

- [github/raven2cz/dotfiles](https://github.com/raven2cz/dotfiles)