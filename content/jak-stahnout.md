---
title: "Jak stáhnou Arch Linux"
date: 2021-12-11
author: "archos"
draft: false
---

### Získejte nejnovější obraz ISO

Nejnovější obraz ISO lze stáhnout ze stránek [Arch Linuxu](https://archlinux.org/download/).

Obraz ISO obsahuje pouze programy nezbytné k instalaci minimálního základního systému GNU / Linux. *Všimněte si, že minimální základní systém neobsahuje grafické uživatelské rozhraní. *Zbytek systému Arch Linux – včetně grafického rozhraní – se nastavuje z příkazové řádky.

### Zkontrolujte obraz ISO

Při stahování přes [torrent](https://archlinux.org/releng/releases/2021.12.01/torrent/) nebo magnetický odkaz je po stažení ISO soubor automaticky zkontrolován na shodu s originálem. Pokud je obraz ISO stažen přes HTTPS, měla by proběhnout kontrola se součtem SHA1. Pokud má být vytvořeno CD nebo DVD, je lepší zkontrolovat shodu až po vypálení na medium.

```
sha1sum archlinux-*-x86_64.iso
```

( ***** musí být nahrazeno datem na staženém souboru Arch.iso.)

### Vypálit obraz ISO na CD nebo DVD

Ze systému Linux to lze provést pomocí aplikací jako k3b, Brasero nebo pomocí příkazu 

```
wodim dev=/dev/sr0 speed=12 -dao -eject -v archlinux-*-x86_64.iso
```

 ***** musí být nahrazeno datem na staženém souboru Arch.iso.)

Po vypálení by měl být kontrolní součet SHA1 na CD/DVD porovnán s informacemi na[ Arch Linux](https://archlinux.org/download/). (Cesta jednotky (sr0) se může lišit v závislosti na zařízení.)

```
sha1sum /dev/sr0
```

### Přenesení ISO obrazu na USB flash disk

Nejprve je třeba určit označení oddílu USB klíče pomocí následujícího příkazu:

```
fdisk -l
```

Soubor ISO lze poté přenést na klíčenku, pomocí příkazu: 

```
dd bs=4M if=/pfad/archlinux-*-x86_64.iso of=/dev/sdx status=progress oflag=sync
```

Použito  [pokynů ](https://wiki.archlinux.de/title/Anleitung_f%C3%BCr_Einsteiger) pro začátečníky.