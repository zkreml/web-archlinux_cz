---
title: "O Arch Linuxu"
date: 2021-12-11
author: "archos"
draft: false
---

**Arch Linux**  je nezávislá [linuxová distribuce](https://cs.wikipedia.org/wiki/Linuxov%C3%A1_distribuce) vytvořená [Juddem Vinetem](https://cs.wikipedia.org/wiki/Judd_Vinet), jenž se inspiroval distribucí CRUX Linux. Arch Linux je vyvíjen jako nenáročný, odlehčený a snadno přizpůsobitelný systém.

![](https://arch-linux.cz/wp-content/uploads/2021/12/external-content.duckduckgo.com_-1.jpg)

Vývoj začal již v roce 2001 a první verzi Archu vydal [Judd Vinet](https://cs.wikipedia.org/wiki/Judd_Vinet) v roce 2002. Ten také byl do roku 2007 hlavním vývojářem. Od roku 2007 je hlavním vývojářem Archu [Aaron Griffin](https://www.Archlinux.org/people/developers/).

Arch je od začátku svého vývoje až do dneška nezávisle vyvíjenou komunitní distribucí.

## Zásady

#### Jednoduchost

Arch je v základu odlehčená a vysoce flexibilní distribuce, která po instalaci poskytuje pouze minimální prostředí bez grafického uživatelského rozhraní. Většina ostatních distribucí nabízí tuto možnost také, ale většinou ne jako hlavní a už vůbec ne jedinou variantu pro instalaci.

#### Modernost

Arch Linux se snaží udržovat nejnovější stabilní verze svého softwaru, pokud lze rozumně zabránit systémovému rozbití balíčků. Je založen na systému [rolling-release](https://en.wikipedia.org/wiki/Rolling_release) , který umožňuje jednorázovou instalaci s průběžnými aktualizacemi.

Arch obsahuje mnoho novějších funkcí dostupných uživatelům GNU/Linuxu, včetně [systemd](https://wiki.archlinux.org/title/Systemd) init systému, moderních [souborových systémů](https://wiki.archlinux.org/title/File_systems) ,  LVM2, softwarového RAID, podpory udev a initcpio (s [mkinitcpio](https://wiki.archlinux.org/title/Mkinitcpio) ), stejně jako nejnovější dostupná jádra.

#### Všestrannost

Arch Linux je univerzální distribuce. Po instalaci je k dispozici pouze prostředí příkazového řádku: namísto trhání nepotřebných a nechtěných balíčků je uživateli nabídnuta možnost vytvořit si vlastní systém výběrem z tisíců vysoce kvalitních balíčků poskytovaných v [oficiálních repozitářích](https://wiki.archlinux.org/title/Official_repositories).

#### Balíčkovací systém

Jako většina jiných distribucí poskytuje Arch správce balíčků, jeho grafické uživatelské nadstavby a sadu oficiálních repozitářů. Kromě toho poskytuje ale i další možnosti: uživatelský repozitář AUR, kde jsou tisíce balíčků, které lze velmi snadno překládat a instalovat pomocí vlastních nástrojů Archu. 

Arch User Repository (AUR) je komunitou řízené úložiště pro uživatele Archu. Obsahuje popisy balíčků ( [PKGBUILDs](https://wiki.archlinux.org/title/PKGBUILD) ), které vám umožňují sestavit balíček ze zdrojového [kódu](https://wiki.archlinux.org/title/Makepkg) pomocí [makepkg](https://wiki.archlinux.org/title/Makepkg) a poté jej nainstalovat přes [pacman](https://wiki.archlinux.org/title/Pacman#Additional_commands) . AUR byl vytvořen, aby organizoval a sdílel nové balíčky z komunity a pomohl urychlit začlenění oblíbených balíčků do [komunitního úložiště](https://wiki.archlinux.org/title/Community_repository) . Tento dokument vysvětluje, jak mohou uživatelé přistupovat a využívat AUR.

Velký počet nových balíčků, které vstupují do oficiálních repozitářů, začíná v AUR. V AUR mohou uživatelé přispívat svými vlastními sestaveními balíčků ( `PKGBUILD`a souvisejícími soubory). Komunita AUR má možnost hlasovat pro balíčky v AUR. Pokud se balíček stane dostatečně populárním – za předpokladu, že má kompatibilní licenci a dobrou balicí techniku ​​– může být vložen do *komunitního* úložiště (přímo přístupné *pacmanem* nebo [abs](https://wiki.archlinux.org/title/Abs) ).