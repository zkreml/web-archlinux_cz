---
title: "Archinstall 4.2 – novinky v instalátoru Arch Linuxu"
date: 2026-04-20
author: "archos"
draft: false
categories: ['Zprávy']
tags: ['archinstall']
---

Archinstall 4.2 je venku a přináší pár zajímavých změn, které stojí za zmínku. Pokud instaluješ Arch přes oficiální textový instalátor, tahle verze ti nabídne jemnější kontrolu nad KDE Plasma, pár vylepšení kolem pacmanu a jeden dost zásadní bezpečnostní fix u šifrovaných instalací.

## Co je Archinstall

Archinstall je oficiální textový instalátor Arch Linuxu, který najdeš přímo na instalačním ISO. Od verze 4.0 běží na frameworku Textual, takže místo starého curses rozhraní máš moderní TUI. Default instalátor na ISO `2026.04.01`.

## Hlavní novinky ve verzi 4.2

### Granulární konfigurace KDE Plasma

Nově si můžeš v instalátoru detailněji poskládat KDE prostředí. Profil Plasma taky konečně instaluje balíček `plasma-meta` místo jen `plasma-desktop`, takže dostaneš kompletní sadu bez doinstalovávání.

### NVIDIA ovladače

Pro mainline kernel se teď používá `nvidia-open` místo `nvidia-open-dkms`. Pokud jedeš custom kernel (LTS, zen, hardened), DKMS varianta zůstává.

### Nové Pacman submenu

V instalátoru přibylo samostatné menu pro pacman, kde si rovnou nastavíš:

- barevný výstup (`Color`)
- paralelní stahování balíčků (`ParallelDownloads`)

Nic, co bys nedokázal hodit do `/etc/pacman.conf` ručně, ale pěkný detail.

### Wayland bez Xorgu

Pokud zvolíš Wayland profil, instalátor už netáhne zbytečně Xorg balíčky. Čistší instalace, menší místo na disku.

## Bezpečnostní fix – šifrované instalace

Tohle je důležité. V předchozích verzích se při šifrování jen `/home` (ale ne rootu) generoval keyfile, který se zapsal na **nešifrovanou root partici**. Jinými slovy – klíč k šifrovanému disku ležel volně dostupný.

Od 4.2 se keyfile generuje **pouze když je šifrovaný i root**. Pokud jsi takovou instalaci dělal ve starší verzi, mrkni na to a případně keyfile smaž nebo reinstaluj.

## Další změny

- konstanty pro `/etc/pacman.conf`, mirrorlist a archiso mountpoint
- refaktor funkcí `copy_iso_network_config()` a `sync_log_to_install_medium()`
- tab nahrazen mezerami v náhledu balíčků
- Enter v multi-select zase funguje jako accept, když nic není vybráno
- podpora prázdných vstupů u mountpointů
- přidané `LPath` execute permission metody
- překlady, dependency bump, cleanup kódu

## Jak updatnout

Pokud bootuješ z aktuálního Arch ISO, stačí:

```bash
# aktualizace archinstall na live ISO
pacman -Sy archinstall

# kontrola verze
archinstall -v
```

Pak spustíš instalátor normálně:

```bash
archinstall
```

## Shrnutí

Archinstall 4.2 není revoluce, ale druhý maintenance release 4.0 série – a hlavně nese důležitý security fix kolem keyfiles u částečně šifrovaných instalací. Pokud plánuješ čerstvou instalaci Archu, rozhodně použij tuhle verzi.

Release notes najdeš na [GitHubu projektu](https://github.com/archlinux/archinstall).