---
title: "Arch Linux – Základní příkazy"
date: 2026-03-26
description: "Praktický průvodce základními příkazy v Arch Linuxu"
tags: ["návody", "arch-linux", "příkazy"]
---

Praktický průvodce pro začátečníky a mírně pokročilé uživatele.

## Správa balíčků

```bash
sudo pacman -Syu           # aktualizace systému
sudo pacman -Syu balíček   # instalace balíčku
sudo pacman -Rns balíček   # odebrání balíčku
pacman -Ss balíček         # hledání balíčku
```

## Systemd

```bash
systemctl status služba
systemctl enable --now služba
journalctl -xe
```
