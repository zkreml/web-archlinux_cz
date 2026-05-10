---
title: "GNOME - Jednoduché, krásné, elegantní."
date: 2022-06-25
author: "archos"
draft: false
tags: ['gnome']
---

![](https://arch-linux.cz/wp-content/uploads/2022/06/gnome-logo.png)

![](https://arch-linux.cz/wp-content/uploads/2022/06/gnome-screenshot1-1024x576.jpg)

![](https://arch-linux.cz/wp-content/uploads/2022/06/gnome-screenshot3-1024x576.jpg)

Další díl seriálu o Arch Linuxu od [Tondy Fischera](https://github.com/raven2cz). V dnešním díle se podíváme  desktopové prostředí Gnome.

## [](https://github.com/raven2cz/tux/tree/main/220501-gnome#gnome---jednoduché-krásné-elegantní-1)GNOME - Jednoduché, krásné, elegantní.

GNOME (*(ɡ)noʊm*, GNU Network Object Model Environment) je desktopové prostředí, jehož cílem je být jednoduché a snadno použitelné. Je navržen [GNOME Project](https://en.wikipedia.org/wiki/The_GNOME_Project) a skládá se výhradně z bezplatného a open-source softwaru. Největším firemním přispěvatelem je **Red Hat**. Výchozí zobrazení je Wayland místo Xorg a dostupné relace jsou

- **GNOME**, výchozí, spouští GNOME Shell na Wayland. Tradiční X aplikace běží přes Xwayland.

- **GNOME Classic** poskytuje „tradiční pracovní prostředí“ (s rozhraním podobným GNOME 2) pomocí určitých rozšíření a hodnot. Jedná se tedy spíše o upravenou formu prostředí GNOME než o skutečně odlišný režim.

- **GNOME na Xorg** spouští prostředí GNOME pomocí Xorg.

### Nostalgie Gnome 2

`GNOME 2.20` je nejnovější verze GNOME Desktop: oblíbené, multiplatformní desktopové prostředí. GNOME se zaměřuje na snadnost použití, stabilitu a prvotřídní podporu internacionalizace a usnadnění. Takto o něm kdysi psali ve zlatém věku Gnome.

![](https://arch-linux.cz/wp-content/uploads/2022/06/gnome2.png)

### Důležité GNOME odkazy

- [GNOME Arch Wiki](https://wiki.archlinux.org/title/GNOME)

- [GNOME Home Page](https://www.gnome.org)

- [Contribution Tutorial](https://wiki.gnome.org/Newcomers/)

- [GNOME DocumentationProject](https://wiki.gnome.org/DocumentationProject)

- [GNOME Source Codes and Report Issues](https://gitlab.gnome.org/explore/groups)

- [GNOME Wiki](https://wiki.gnome.org/Home)

- [GNOME Developer Site](https://developer.gnome.org/)

### GNOME Instalace

Sledujte stránku [Arch Wiki Gnome](https://wiki.archlinux.org/title/GNOME). Přečtěte si podrobnosti o krocích instalace.

Nainstalujte základní a doplňkové komponenty. Poté Gnome Extensions (rozšíření gnome) a nainstalujte volitelná rozšíření.

```
paru -S gnome gnome-extra
# Optional Dependencies
paru -S chrome-gnome-shell-git
paru -S gnome-shell-extension-pop-shell-git --overwrite '*'
/usr/share/gnome-shell/extensions/pop-shell@system76.com/scripts/configure.sh
pop-shell-shortcuts
```

Spouštěč gnome je připraven v mém `.xinitrc`, který používáme v celé naší sérii. Viz odkaz `.dotfiles` níže pro Github. Takže vše, co musíte udělat, je spustit `startx ~/.xinitrc gnome`, nebo pomocí správce zobrazení vybrat `xinitrc-gnome` ze souborů mých relací v adresáři `.root`.

### GNOME Volitelná rozšíření

Tato rozšíření používám pro náš demo projekt. Nainstalujte rozšíření Gnome z [https://extensions.gnome.org/#](https://extensions.gnome.org/#)

**GNOME Seznam Rozšíření**

- Dash to Panel

- Fly-Pie

- System-monitor-next

- Unite

- Pop Shell

- Několik vestavěných rozšíření: Pamac Updates Indicator, Places Status Indicator, Workspace Indicator, Applications Menu

### GNOME Fly-Pie Extension

![](https://arch-linux.cz/wp-content/uploads/2022/06/fly-pie-1024x233.jpg)

Zde je video ukázka [Fly-Pie Intro](https://www.youtube.com/watch?v=BGXtckqhEIk).

Fly-Pie je rozšíření pro GNOME Shell, které umožňuje otevírat nabídky označení pomocí klávesových zkratek. A — podle mého nejlepšího vědomí — je to **první rozšíření GNOME Shell s úspěchy!** ![](https://github.githubassets.com/images/icons/emoji/unicode/1f3c6.png)

Přidejte toto rozšíření fly-pie do svého projektu, nainstalujte jej.

Konfigurace, spusťte aplikaci Rozšíření, vyberte tlačítko Konfigurace Fly-Pie. Nakonfigurujte si nabídky fly-pie a zkratku aktivity pomocí `ctrl+mezera` a `super+myš-pravé-tlačítko`.

### GNOME Pop!_OS Shell Rozšíření

https://www.youtube.com/watch?v=-fltwBKsMY0

Zdrojový kód [zde](https://github.com/pop-os/shell). Nyní funguje s GNOME >=42.

Představil System76. Zaměřte se na [Pop!_OS Page](https://pop.system76.com/).

[Auto-Tiling Pop!_OS feature here.](https://www.youtube.com/watch?v=-fltwBKsMY0)

[Stacking support here.](https://www.youtube.com/watch?v=1TSdFWY_U9A)

https://www.youtube.com/watch?v=1TSdFWY_U9A

Úplnou konfiguraci a ovládání naleznete v našem videu.

![](https://arch-linux.cz/wp-content/uploads/2022/06/gnome-screenshot3-2-1024x576.jpg)

![](https://arch-linux.cz/wp-content/uploads/2022/06/2-1024x576.jpg)

### GNOME Konfigurace prostředí

![](https://arch-linux.cz/wp-content/uploads/2022/06/3-1024x576.jpg)

Nakonfigurujte doporučená rozšíření a přizpůsobte prostředí Gnome. Viz video.

Konečně se dostaneme k horním snímkům obrazovky

### GNOME Ergonomické nastavení

Rozšíření shellu Pop!_OS přepíše zkratky voláním `/usr/share/gnome-shell/extensions/pop-shell@system76.com/scripts/configure.sh` výchozí zkratky. Nyní musíme nakonfigurovat a překonfigurovat zkratky do naší ergonomické podoby.

Původní nastavení prostředí Pop!_OS: `pop-shell-shortcuts`

![](https://arch-linux.cz/wp-content/uploads/2022/06/popos-shell-shortcuts-default-464x1024.jpg)

**Seznam našich změn** Výběr `Gnome Settings > Keyboard > Keyboard Shortcuts`

- Accessibility

Default

- Launchers

Default

- Move, size, and swap windows / Přesun, velikost a výměna oken

Adjustment mode [ctrl+super+return], remove default [super+return]

- All next is same

- Navigate applications and windows / Procházení aplikací a oken

Launch and switch applications [super+s], remove [super+/]

- Navigation

Move window to left and right [shift+super+left/right]

- Switch to workspaces: [super+F1,…F4]

- Move to workspace left and right [super+left/right], or default [ctrl+alt+left/right]

- Screenshots

Default

- Sound and Media

Default

- System

Default

- Tiling

Default

- Typing

Switch to next input source [alt+space],[super+space] (alt+shift nemůže být v gnome použit!)

- Windows

Window menu [alt+space]

- Close window [shift+super+c]

- Toggle fullscreen mode [super+f]

- Toggle maxmization state [super+m]

- Custom Shortcuts

Alacritty [super+return]

- kitty [super+alt+return]

https://www.youtube.com/watch?v=cNmYBWblra0&t=1555s

### Důležité odkazy

- [Youtube Channel TUX: Svět Linuxu](https://www.youtube.com/user/tondafischer/featured)

- [Forum Arch Linux CZ](https://forum.arch-linux.cz/)

- [Arch Linux CZ](https://arch-linux.cz/)

- [archlinux.org](https://archlinux.org/)

- [wiki.achlinux.org](https://wiki.archlinux.org/)

- [fishlive.org/blog](https://fishlive.org/en/blog-tech-art/arch)

- [github/raven2cz/tux](https://github.com/raven2cz/tux)

- [github/raven2cz/dotfiles](https://github.com/raven2cz/dotfiles)

- [raven2cz/public-wallpapers](https://github.com/raven2cz/public-wallpapers)

- [raven2cz/global-colorschemes](https://github.com/raven2cz/global-colorscheme)