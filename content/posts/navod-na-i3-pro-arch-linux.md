---
title: "Návod na i3 pro Arch Linux"
date: 2024-12-06
author: "archos"
draft: false
categories: ['Arch Linux']
tags: ['I3']
---

## Úvod do i3

i3 je dynamický správce oken, který je určen pro pokročilé uživatele, kteří chtějí mít plnou kontrolu nad rozvržením svého desktopového prostředí. i3 je velmi flexibilní a umožňuje přizpůsobení pomocí klávesových zkratek, skriptů a konfigurací.

Výhody i3:

- Minimalistické a rychlé prostředí.
- Plně přizpůsobitelné.
- Podpora pro více monitorů a workspace.
- Výborné pro efektivní multitasking a produktivitu.

Proč zvolit i3:

- Pokud chcete mít plnou kontrolu nad svým pracovním prostředím.
- Pokud vám nevyhovují tradiční desktopová prostředí jako GNOME nebo KDE.
- Pokud preferujete práci s klávesovými zkratkami a dlaždicovým rozvržením.
![](https://arch-linux.cz/wp-content/uploads/2024/12/Snimek-obrazovky-porizeny-2024-12-06-08-10-36-300x169.png)

## Instalace i3 na Arch Linux

Pro instalaci i3 na Arch Linux použijte následující příkazy:

```bash
sudo pacman -S i3-wm i3-gaps dmenu
```

To nainstaluje i3, i3-gaps (pro přizpůsobení mezer mezi okny) a dmenu (program pro spuštění aplikací). Po instalaci můžete spustit i3 příkazem:

## Základní konfigurace

Po instalaci i3 je potřeba nakonfigurovat konfigurák, který se nachází v adresáři `~/.config/i3/config`. Tento soubor obsahuje výchozí nastavení, které můžete upravit podle svých potřeb.

#### Výchozí konfigurace obsahuje:

- Nastavení klávesových zkratek pro navigaci mezi okny a workspace.
- Výběr vzhledu (okna, panely, motivy).
- Možnost přizpůsobit spouštění aplikací.

### Příklad základní konfigurace:

#### Nastavení mod klávesy

```bash
set $mod Mod4
```

#### Klávesové zkratky pro přepínání mezi workspace

```bash
bindsym $mod+1 workspace 1
bindsym $mod+2 workspace 2
# atd.
```

## Klávesové zkratky a navigace

i3 používá klávesové zkratky pro efektivní ovládání systému. Zde jsou některé základní zkratky:

## Klávesové zkratky pro i3

Akce
Klávesová zkratka

Otevřít terminál
`$mod+Enter`

Zavřít aktuální okno
`$mod+q`

Otevřít dmenu
`$mod+d`

Přejít na workspace 1
`$mod+1`

Přejít na workspace 2
`$mod+2`

Přejít na workspace 3
`$mod+3`

Přejít na workspace 4
`$mod+4`

Přejít na workspace 5
`$mod+5`

Přejít na workspace 6
`$mod+6`

Přejít na workspace 7
`$mod+7`

Přejít na workspace 8
`$mod+8`

Přejít na workspace 9
`$mod+9`

Přejít na workspace 10
`$mod+0`

Přesunout okno na workspace 1
`$mod+Shift+1`

Přesunout okno na workspace 2
`$mod+Shift+2`

Přesunout okno na workspace 3
`$mod+Shift+3`

Přesunout okno na workspace 4
`$mod+Shift+4`

Přesunout okno na workspace 5
`$mod+Shift+5`

Přesunout okno na workspace 6
`$mod+Shift+6`

Přesunout okno na workspace 7
`$mod+Shift+7`

Přesunout okno na workspace 8
`$mod+Shift+8`

Přesunout okno na workspace 9
`$mod+Shift+9`

Přesunout okno na workspace 10
`$mod+Shift+0`

Přepnutí do plovoucího režimu
`$mod+Shift+space`

Zpět na dlaždicové okno
`$mod+space`

Maximální okno (fullscreen)
`$mod+f`

Vertikální rozdělení oken
`$mod+v`

Horizontální rozdělení oken
`$mod+h`

Přepnutí mezi okny vlevo
`$mod+j` nebo `$mod+Left`

Přepnutí mezi okny vpravo
`$mod+k` nebo `$mod+Right`

Přepnutí mezi okny nahoru
`$mod+b` nebo `$mod+Up`

Přepnutí mezi okny dolů
`$mod+o` nebo `$mod+Down`

Přejít na předchozí okno
`$mod+Tab`

Přejít na další okno
`$mod+Shift+Tab`

Přepnout na předchozí workspace
`$mod+Shift+Tab`

Otevřít menu pro aplikace
`$mod+d`

Zavřít okno
`$mod+q`

Získat aktuální stav systému
`$mod+Shift+c`

Restartovat i3 bez ztráty konfigurace
`$mod+Shift+r`

## Práce s plovoucími okny

Plovoucí okna vám umožní mít okna, která nejsou v dlaždicovém rozvržení. Pro přepnutí mezi dlaždicovým a plovoucím režimem použijte následující klávesovou zkratku:

```
bindsym mod+Shift+space floating toggle
```

To umožní oknu přepnout mezi plovoucím a dlaždicovým režimem.

## Jak přepínat mezi okny:

- **mod+j, mod+k, mod+Left, mod+Right**: Přepnutí mezi okny v rámci jednoho workspace.

## Pokročilé techniky

### Přiřazování aplikací na workspace:

Můžete přiřadit aplikace na specifické workspace podle jejich třídy nebo instance:

```bash
assign [class="Firefox"] $ws2
assign [class="Xfce4-terminal"] $ws1
```

Tímto způsobem bude Firefox vždy otevřený na workspace 2 a terminál na workspace 1.

## Automatické spouštění aplikací:

Pro automatické spuštění aplikací při startu i3 přidejte příkazy do konfiguračního souboru:

```bash
exec --no-startup-id picom -b  # Spuštění compositoru pro průhlednost
exec --no-startup-id nm-applet  # Spuštění appletu pro správu sítě
```

## Užitečné tipy a triky

- Používejte i3bar pro zobrazení systémových informací, např. CPU, paměť, čas.
- Používejte dmenu nebo rofi pro rychlé vyhledávání aplikací.
- Udržujte svůj konfigurák čistý a dobře organizovaný pro snadné přizpůsobení.

## Závěr

i3 je skvělý správce oken pro pokročilé uživatele, kteří chtějí maximálně přizpůsobit své pracovní prostředí. Doufám, že tento návod vám pomůže začít s i3 na Arch Linuxu a využít jeho plný potenciál.

## Zdroj a další informace

Pro více informací o správci oken i3 a jeho vývojářích můžete navštívit oficiální stránky:

- [Oficiální web i3](https://i3wm.org/)
- [GitHub repozitář i3](https://github.com/i3/i3)