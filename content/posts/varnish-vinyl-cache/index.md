---
title: "Arch News: Varnish se přejmenoval na Vinyl Cache"
date: 2026-05-25
draft: false
tags: ["news", "varnish", "migrace"]
image: "varnish-cache.jpg"
---

{{< figure src="varnish-cache.jpg" alt="Varnish Cache" >}}

Pokud na svém systému provozuješ reverzní proxy nebo HTTP cache postavenou na Varnishi, pozor — upstream projekt se přejmenoval na **Vinyl Cache** a Arch ho následoval. Balíček `varnish` byl odstraněn z repozitáře `[extra]` a nahrazen novým balíčkem `vinyl-cache`.

Změna není jen kosmetická. Přejmenovaly se binárky, adresáře, systemd jednotky i systémoví uživatelé. Po upgradu je nutná ruční migrace.

---

## Co se změnilo

| Staré | Nové |
|---|---|
| `/etc/varnish` | `/etc/vinyl-cache` |
| `/var/lib/varnish` | `/var/lib/vinyl-cache` |
| `varnish.service` | `vinyl-cache.service` |
| `varnishncsa.service` | `vinylncsa.service` |
| uživatel `varnish` | uživatel `vinyl` |
| skupina `varnish` | skupina `vinyl` |
| uživatel `varnishlog` | uživatel `vinyllog` |
| uživatel `vcache` | beze změny |

---

## Postup migrace

```bash
# 1. nainstaluj nový balíček
sudo pacman -Syu vinyl-cache

# 2. přejmenuj adresáře
sudo mv /etc/varnish /etc/vinyl-cache
sudo mv /var/lib/varnish /var/lib/vinyl-cache

# 3. oprav vlastnictví souborů
sudo chown -R vinyl:vinyl /var/lib/vinyl-cache

# 4. vypni staré systemd jednotky, zapni nové
sudo systemctl disable --now varnish.service varnishncsa.service
sudo systemctl enable --now vinyl-cache.service vinylncsa.service

# 5. zkontroluj stav
systemctl status vinyl-cache.service
journalctl -u vinyl-cache.service -n 30
```

---

## Poznámky

- Arch momentálně neplánuje udržovat balíček `varnish` jako samostatný fork — jedinou podporovanou cestou je přechod na `vinyl-cache`.
- Pokud máš v konfiguraci reference na staré cesty nebo názvy uživatelů, je potřeba je ručně opravit.
- Detailní přehled breaking changes najdeš v [arch-announce mailing listu.](https://lists.archlinux.org/archives/list/arch-announce@lists.archlinux.org/thread/4BSRLLGJ5552NASTYKCDZ3Q6DIMW2J4J/).
