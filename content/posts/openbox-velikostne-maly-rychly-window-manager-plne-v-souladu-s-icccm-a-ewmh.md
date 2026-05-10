---
title: "Openbox- velikostně malý, rychlý window manager plně v souladu s ICCCM a EWMH"
date: 2022-05-21
author: "archos"
draft: false
categories: ['Návody']
tags: ['openbox']
---

![](https://arch-linux.cz/wp-content/uploads/2022/05/openbox-screen-1024x576.jpg)

#### Openbox - velikostně malý, rychlý window manager plně v souladu s ICCCM a EWMH

 V dalším díle seriálu Tondy Fischera, se podíváme na instalaci a nastavení správce oken Openbox.

Openbox je vysoce konfigurovatelný správce oken s rozsáhlou podporou standardů ICCCM a EWMH.

- Vizuální styl `*box` je dobře známý pro svůj minimalistický vzhled. Openbox používá vizuální styl `*box` a zároveň poskytuje větší počet možností pro vývojáře témat než předchozí implementace `*box`. Dokumentace k tématu popisuje celou řadu možností, které lze nalézt v Openbox tématech.

- Openbox vám umožňuje přenést nejnovější aplikace mimo plnohodnotné desktopové prostředí. Většina moderních aplikací byla napsána s ohledem na GNOME a KDE. S podporou standardů freedesktop.org a pečlivým dodržováním předchozích standardů poskytuje Openbox prostředí, kde aplikace fungují tak, jak byly navrženy.

- Openbox vám umožňuje změnit téměř každý aspekt vaší interakce s vaším desktopem a vymýšlet zcela nové způsoby, jak jej používat a ovládat. Pro ovládání oken to může být jako videohra. Ale Openbox může být také extrémně jednoduchý, protože je ve výchozím nastavení, což znamená, že může vyhovovat téměř každému. Openbox vám dává kontrolu, aniž byste museli dělat všechno.

- Openbox vylepšuje desktopová prostředí. Spuštěním Openboxu v GNOME nebo KDE můžete spojit jejich snadnost a funkčnost se silou Openboxu. Když používáte Openbox, vaše plocha bude čistší a rychlejší a máte ji pod kontrolou.

- Podívejte se na příručku Začínáme a změňte způsob správy pracovní plochy. Viz hlavní stránky [openbox.org](http://openbox.org/wiki/Main_Page).

- **Oficiální dokumentace Openboxu** je [zde](http://openbox.org/wiki/Help:Contents).

#### Openbox Instalace

Prostudujte stránku [Arch Wiki Openbox](https://wiki.archlinux.org/title/Openbox). Přečtěte si podrobnosti o krocích instalace a komponentách OB.

```
paru -S openbox ttf-dejavu ttf-liberation obfilebrowser
# Optional Dependencies
paru -S picom nitrogen tint2 polybar volctl clipmenu parcellite xfce4-notify
```

Než začnete, upravte svůj `~/.config/openbox/autostart`, definujte své služby a aplikace, které budou použity s relací openboxu.

Výchozí nastavení Openboxu - použijte tyto příkazy

```
$ mkdir -p ~/.config/openbox
$ cp -a /etc/xdg/openbox/ ~/.config/
```

Pokud plánujete používat můj projekt openbox, postupujte podle pokynů v [GitHub Openbox Project](https://github.com/raven2cz/openbox-config).

```
git clone git@github.com:raven2cz/openbox-config.git ~/.config/openbox
```

Spouštěč openboxu je připraven v mém `.xinitrc`, který používáme v celé naší video sérii. Viz níže uvedený odkaz `.dotfiles` pro Github. Takže vše, co musíte udělat, je spustit `startx ~/.xinitrc openbox` nebo použít správce zobrazení k výběru `xinitrc-openbox` ze souborů mých sessions (relací) v adresáři `.root`.

#### Openbox Lego

Nejlepší a rychlé čtení je [Arch Wiki Openbox](https://wiki.archlinux.org/title/Openbox), začněte od něj. Dokumentace k Openboxu je [zde](http://openbox.org/wiki/Help:Contents).

Můj příklad lega (sada komponentů) je následující:

- **WM:** openbox-session s automatickým spuštěním a soubory prostředí

- **Kompositor:** picom

- **Bar:** polybar [polybar-config](https://github.com/raven2cz/polybar-config)

- **Conky:** [MX-CoreBlue](https://github.com/raven2cz/dotfiles/tree/main/.config/conky/MX-CoreBlue)

- **Menu:** static menu openbox, podpora generátorů a pipes menu, obfilebrowser

- **Navigace:** rofi, [rofi-themes](https://github.com/raven2cz/rofi-themes)

- **Wallpaper app:** nitrogen

- **Zvukový systém:** [volctl](https://github.com/buzz/volctl)

- **Notifikační služba:** xfce4-notify

- **Wallpaper:** [public-wallpapers](https://github.com/raven2cz/public-wallpapers) - [tapeta openbox](https://github.com/raven2cz/public-wallpapers/blob/main/00046- openbox-1.jpg)

Máte mnoho možností, jak vybrat různé lego. Máte-li k tomuto tématu další dotazy; Issue můžete vytvořit pro Github nebo o něm diskutovat na [forum](https://forum.arch-linux.cz/category/26/openbox).

#### Openbox Ergonomic Settings

Všechny klávesové zkratky musí být přidány do souboru `~/.config/openbox/rc.xml` a pod nadpis ``. Ačkoli zde byl uveden stručný přehled, podrobnější vysvětlení klávesových zkratek lze nalézt na [openbox.org](http://openbox/org).

Klávesové zkratky lze přidat do konfiguračního souboru pomocí následující syntaxe:

```

  
    ...
  

```

Název akce pro spuštění externího příkazu je `Execute`. K definování externího příkazu, který se má provést, použijte následující syntaxi:

```

  my-command

```

Seznam všech dostupných akcí naleznete na [Openbox wiki](http://openbox.org/wiki/Help:Actions).

Kompletní ergonomická nastavení jsou připravena v mém [GitHub Openbox Project](https://github.com/raven2cz/openbox-config) v `rc.xml`. Kompletní průvodce a manipulace je vysvětlena ve videu. Ergonomie odpovídá předchozí sérii videí pro ostatní WM.

#### Openbox Výkonná Menu

Hlavní předností `*box` jsou výkonná a kvalitní menu. Celé ovládání tohoto WM je založeno na nabídkách a menu.

V Openboxu je možné použít tři typy menu: `static`, `pipes (dynamické)` a `generátory (statické nebo dynamické)`. Mohou být také použity samostatně nebo v jakékoli kombinaci. Více podrobností v OB Docs a [Arch Wiki](https://wiki.archlinux.org/title/Openbox#Menus).

Pro náš příklad jsem použil aktualizovanou strukturu menu v souboru `menu.xml`. Kromě toho je zde použití menu pipes s aplikací `obfilebowser` pro procházení vaší domovské složky - aktualizujte soubor `menu.xml` nabídky a upravte jej podle vašich požadavků.

https://www.youtube.com/watch?v=E2aQfZNbPF0&t=7s

#### Důležité odkazy

- [Youtube Channel TUX: Svět Linuxu](https://www.youtube.com/user/tondafischer/featured)

- [Forum Arch Linux CZ](https://forum.arch-linux.cz/) - naše české forum pro Arch!

- [Arch Linux CZ](https://arch-linux.cz/) - spuštění web server pro Arch

- [archlinux](https://archlinux.org/)[.org](https://archlinux.org/)

- [wiki.achlinux.org](https://wiki.archlinux.org/)

- [fishlive.org/blog](https://fishlive.org/en/blog-tech-art/arch)

- [github/raven2cz/tux](https://github.com/raven2cz/tux)

- [github/raven2cz/dotfiles](https://github.com/raven2cz/dotfiles)

- [raven2cz/public-wallpapers](https://github.com/raven2cz/public-wallpapers)

- [raven2cz/global-colorschemes](https://github.com/raven2cz/global-colorscheme)