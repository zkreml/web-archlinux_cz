---
title: "Bezpečnostní incident: škodlivé balíčky v AUR"
date: 2026-06-12
draft: false
tags: ["aur", "bezpečnost", "arch linux"]
categories: ["Zprávy"]
summary: "Arch Linux tým oznámil aktivní bezpečnostní incident v AUR. Bylo detekováno velké množství škodlivých adoptací a aktualizací balíčků."
---

Arch Linux tým dnes oznámil aktivní bezpečnostní incident v AUR (Arch User Repository).

V repozitáři bylo detekováno velké množství škodlivých adoptací a aktualizací balíčků. Tým aktivně pracuje na jejich identifikaci a zamezení dalších škodlivých commitů.

## Co to znamená pro tebe

Dočasně mohou být omezeny tyto funkce AUR:

- registrace nových účtů
- push aktualizací balíčků
- adopce a vytváření nových balíčků

**Před každou aktualizací AUR balíčku pečlivě zkontroluj PKGBUILD a install skripty** – platí to vždy, ale teď obzvlášť.

Pokud narazíš na podezřelý commit, nahlásit ho můžeš na mailing listu `aur-general`.

Zdroj: [archlinux.org](https://archlinux.org/news/active-aur-malicious-packages-incident/)

## Aktualizace 13. 6. 2026

Arch tým zveřejnil [seznam podezřelých balíčků](https://md.archlinux.org/s/SxbqukK6IA) – obsahuje tisíce položek (mnoho z nich jsou opuštěné nebo dlouhodobě neudržované balíčky, ne nutně škodlivé).

### Jak zkontrolovat svůj systém

Stáhni si seznam a porovnej s nainstalovanými AUR balíčky:

```bash
curl -s https://md.archlinux.org/SxbqukK6IA/download > /tmp/aur-bad.txt
pacman -Qm | awk '{print $1}' | grep -Fxf /tmp/aur-bad.txt
```

Pokud nic nevypíše, jsi v bezpečí. Pokud něco vypíše, doporučuji balíček odebrat:

```bash
yay -Rns nazev-balicku
```

Pro důkladnou kontrolu systému můžeš použít:

```bash
sudo pacman -S chkrootkit
sudo chkrootkit
```
