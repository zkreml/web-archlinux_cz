---
title: "Neplatné podpisové klíče během aktualizace systému"
date: 2022-05-06
author: "archos"
draft: false
categories: ['Naše komunita']
tags: ['update']
---

V současné době existují některé podpisové klíče pro balíčky Arch, které jsou při aktualizaci detekovány jako neplatné (vypršela platnost, byly staženy atd.). To způsobí, že aktualizace systému pomocí Pacmana selže.

```
error: 
: signature from "Someone " is marginal trust
:: File /var/cache/pacman/pkg/_x86_64.pkg.tar.zst is corrupted (invalid or corrupted package (PGP signature)).
Do you want to delete it? [Y/n]
```

Je třeba nejprve aktualizovat podpisové klíče a potom systém.

```
sudo pacman -Sy archlinux-keys
sudo pacman -Syu
```