---
title: "Nový Arch Linux ISO s kernelem 6.16"
date: 2025-09-01
author: "archos"
draft: false
categories: ['Arch Linux']
tags: ['iso', 'archlinux']
---

# Nový Arch Linux ISO s kernelem 6.16

**1. září 2025** - Je tu nový Arch Linux ISO snapshot pro září 2025, první který běží na **Linux kernelu 6.16**. Hlavní novinky:

## Co je nového

### Linux Kernel 6.16

- Lepší detekce hardware, zejména na novějších zařízeních
- Vylepšená podpora i pro starší komponenty, kde předchozí ISO selhávala
- Obecně stabilnější základ systému

### Archinstall 3.0.9

Nová verze instalátoru přináší několik užitečných funkcí:

- **LUKS iteration time** - možnost změnit čas iterací pro šifrování
- **U2F autentifikace** - podpora pro hardware klíče
- **Bluetooth během instalace** - nastavení BT spojení přímo v instalátoru
- **`--skip-boot` parametr** - přeskočení instalace bootloaderu
- **Lepší COSMIC podpora** - vylepšená integrace nového DE
- **Btrfs + GRUB combo** - automatická instalace `inotify-tools` a `grub-btrfs`

## Pro koho je určený

- **Nové instalace** - pokud chystáš čistou instalaci
- **Rescue situace** - pro opravy systému
- **Hardware testing** - nový kernel může rozchodit problémové komponenty

Existující Arch systémy aktualizuješ klasicky:

```bash
sudo pacman -Syu
```

### Stažení

ISO je dostupný na oficiálních stránkách [Arch Linuxu](https://archlinux.org/download/). Snapshot obsahuje všechny balíčky aktualizované během srpna 2025.