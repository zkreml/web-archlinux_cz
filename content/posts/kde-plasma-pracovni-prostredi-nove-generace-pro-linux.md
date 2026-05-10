---
title: "KDE Plasma - Pracovní prostředí nové generace pro Linux"
date: 2022-04-30
author: "archos"
draft: false
categories: ['Návody']
tags: ['KDE']
---

![](https://arch-linux.cz/wp-content/uploads/2022/04/kde-1-1024x576.jpg)

![](https://arch-linux.cz/wp-content/uploads/2022/04/kde-bismuth-1024x576.jpg)

English document variant [here](https://github.com/raven2cz/tux/blob/main/220327-kde/kde-en.org).

### KDE - Pracovní prostředí nové generace pro Linux

V dalším díle seriálu [Tondy Fischera](https://github.com/raven2cz) si ukážeme instalaci grafického prostředí KDE.

Mocné, multiplatformní a pro všechny. Používejte software KDE pro brouzdání na webu, komunikaci s kolegy, přáteli a rodinou, spravování svých souborů, poslech hudby a sledování videí nebo pro kreativní a produktivní práci. Komunita KDE vyvíjí a udržuje více než 200 aplikací, které běží na kterémkoliv počítači s Linuxem a často i na jiných platformách.

Takto je představováno KDE na svých hlavních stránkách [kde.org](https://kde.org/cs/). Určitě lze souhlasit, že KDE patří mezi velmi dobrá plná desktopová prostředí. Společně s Gnome tvoří pár základních DE, které používají hlavní masy uživatelů GNU/Linux. Plně konfigurovatelné pomocí GUI s mnoha grafickými efekty pomocí kwin. Konfigurovatelnost tohoto DE je daleko značnější než zmiňovaný Gnome, který naopak má uživateli přinést lehkost a jednoducho použití bez nutných zdlouhavých nastavování.

O efektivitě práce, ergonomičnosti a snížení přehmatů na myš a zpět jsme již v tomto seriálu povídali mnohokrát. Každý kdo prošel tímto kurzem již ví, že efektivita se skrývá někde jinde a je potřeba se k ní postupně dopracovat. Samozřejmě je možné toto do určitého stavu dosáhnout i pomocí KDE a jeho schopností konfigurace. Pojďme se tedy podívat na triky a tipy, jak si KDE upravit z hlediska ergonomie a efektivity práce, rovněž umožnit použití KDE aplikací v ostatních DE a WM prostředích se správným nastavením a theme.

### [](https://github.com/raven2cz/tux/tree/main/220327-kde#instalace-kde)Instalace KDE

Nejprve je potřeba KDE nainstalovat. KDE obsahuje tisíc balíčků, z toho důvodů je možné použít skupinu (group) nebo meta skupinu (meta). Rozdíl mezi tímto způsobem viz [meta package and package group](https://wiki.archlinux.org/title/Meta_package_and_package_group). Já zde použiji starší způsob s group, ale klidně použijte novější meta balík.

Za druhé je nutné instalovat skupinu KDE aplikací, které budete chtít používat, nebo nemusíte, záleží na Vás. Opět zde je již možnost group a meta balíku, nebo si vybrat pouze část z meta-balíku, kterou nainstalujete samostatně. V případě instalace waylandu je potřeba ještě instalovat podporu pro wayland. Zde již musím ale odkázat do důkladné přečtění arch wiki a závislé stránky wayland [Arch Wiki KDE](https://wiki.archlinux.org/title/KDE)

```
# egl-wayland just for Nvidia cards, not necessary for AMD
sudo pacman -S plasma kde-applications plasma-wayland-session eql-wayland
# next variants:
sudo pacman -S plasma-meta kde-applications-meta
sudo pacman -S plasma-meta kde-utilities-meta kde-network-meta kde-multimedia-meta
```

.Spouštěč pro X11 a wayland je již připraven v mém `.xinitrc`, který používáme v celém našem seriálu. Viz dolní odkaz .dotfiles na Githubu. Stačí tedy pouze s příkazové řádky spustit `startx ~/.xinitrc kde`, nebo pomocí display manageru vybrat `xinitrc-kde` z mých sessions souborů v adresáři `.root`.

### Qt5ct a Kvantum Manager

Pro plnou podoporu témat je nutné doinstalovat Kvantum Manager. Pro podporu KDE aplikací pro ostatní WM a DE je vhodné Kvantum Manager napojit na qt5ct a konfiguraci donastavit v Qt5 Config aplikaci.

```
paru -S qt5ct kvantum

# Environment variables settings (e.g.in .xinitrc)
export QT_QPA_PLATFORMTHEME=qt5ct
export DESKTOP_SESSION=plasma
export XDG_CURRENT_DESKTOP=kde
```

### Použití grafických témat

System Settings > Global Theme > Get New Global Themes > Install `Layan`. Další možnosti `Arc Dark, Sweet-Mars, Nordic`. Je však ale nezbytné na google dohled příslušné theme (často github repository) a klonovat si jej, protože bude nutné naimportovat potřebnou část pro Kvantum Manager, bez toho se bohužel neobjedneme a toto není součástí standardní instalace v System Settings!

Přepnout globální schéma na `Layan`. Nyní již budeme moci přenastavit barvené schéma, fonty, ikony, windows dekorace atd., viz video pro detaily.

### Přizpůsobení základních komponent pro práci

Nyní již můžeme plně nakonfigurovat veškeré komponenty KDE, aby vyhovovaly našim potřebám. Nebude nic přehánět, KDE lze konfigurovat velmi mocně, budeme se držet opět zlaté střední cesty, která navíc nebude ani tolik náchylná na možné chyby při dalších updates KDE, což bohužel bývá častá příčina najednou vzniklých problémů.

Přizpůsobíme:

- Hlavní panel a jeho komponenty

- HiDpi a fonty

- Pozadí

- Desktopy pro práci

### Bismut - Tiling Support pro KDE

[Bismit Github Link](https://github.com/Bismuth-Forge/bismuth)

Přidání podpory pro tiling (dlaždicové) uspořádání oken. Velmi pokročilý a flexiblní rozšíření KDE.

- System Settings > Window Behaviour > Focus > `Focus follows mouse` (fokus okna následuje myš)

- Window Management > Window Tiling > Enable window tiling (zaškrtnout), záložka Appearance (nahoře) > Inner Gaps nastav na `10px`

- Shortcuts > Window Tiling > Push Active to Master Area nastav: `Meta + Shift + Return`

### Ergonomické nastavení klávesových zkratek

Nejvíce změn. KDE není přípraveno na vhodné ovládání klávesnicí. Viz zejména video nahrávka.

- Shortcuts > Kwin > nastavit Close Window, Quick Tile Window (všechny směry), Maximize, Minimize, Fullscreen window (nastavit vše dle AwesomeWM viz minulé nahrávky)

- Shortcuts > KRunner > přidat `Alt+Space` nebo `Meta+Space` (doporučeno Meta)

- Shortcuts > stiskni tlačítko Add Application > přidat Konsole > Konsole řádka nastavit `Alt+Return` nebo `Meta+Return` (doporučeno Meta)

### Úvahy nad možnými vylepšeními

- KDE lze vylepšovat mnoha způsoby. Často velmi žádané nastavení je MacOS, kde je horní panel zároveň použit jako menu pro aplikace a aplikace tak nemají žádné menu, které je přehozeno do tohoto panelu. I toto KDE umožňuje.

- Jakékoliv větší rozšíření nebo změna přináší potenciální problémy po upgrade KDE. Toto není AwesomeWM API a framework, který si můžete konfigurovat, již mnohokrát jsem se v minulosti setkal s tím, že KDE spadlo nebo celá funkcionalita přestala fungovat. Stabilita KDE je daleko horší pokud provádíte příliš mnoho customizací. Buďte tedy s tím opatrní a pokud chcete velké změny je lepší zvolit WM s programovými dovednostmi.

- Při zvolení některých uživatelských komponent nebo dokonce témat může vzniknout silný performance problém, naposledy Dracula schéma snížilo rapidně animace a maximalizace oken, proto si vždy funkcionalitu nejprve ověřte na Breeze tématu a teprve potom použijte customized řešení pro porovnání.

- Pozor na některé widgets. Celkově mnoho widgets je velmi zastaralých a tedy mohou mít silné performance dopady. Opět ověřte zátež na procesor, snižte taky časové cykly pro čtení hodnot.

- Wayland vs X11. KDE je již plně připraveno na wayland. Mnoho uživatelů zejména hráčů přešlo na wayland. Původně jsem tuto nahrávku chtěl dělat čistě na waylandu, ale HiDpi 4K rozhodně není připraveno, mnoho drobných věcí nefunguje správně a problémy se základními aplikacemi. Hodně času jsem nad tím strávil, ale rozhodně toto nemohu zatím doporučit nováčkům. Toto se může rychle změnit za další “roky”.

https://www.youtube.com/watch?v=vclZ7RSdzoQ&t=1718s

# Důležité odkazy

- [Youtube Channel TUX: Svět Linuxu](https://www.youtube.com/user/tondafischer/featured)

- [Forum Arch Linux CZ](https://forum.arch-linux.cz/) - naše české forum pro Arch!

- [Arch Linux CZ](https://arch-linux.cz/) - spuštění web server pro Arch

- [archlinux.org](https://archlinux.org/)

- [wiki.achlinux.org](https://wiki.archlinux.org/)

- [fishlive.org/blog](https://fishlive.org/en/blog-tech-art/arch)

- [github/raven2cz/tux](https://github.com/raven2cz/tux)

- [github/raven2cz/dotfiles](https://github.com/raven2cz/dotfiles)

- [raven2cz/public-wallpapers](https://github.com/raven2cz/public-wallpapers)

- [raven2cz/global-colorscheme](https://github.com/raven2cz/global-colorscheme)