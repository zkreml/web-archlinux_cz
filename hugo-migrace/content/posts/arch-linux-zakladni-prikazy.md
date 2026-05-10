---
title: "Arch Linux – Základní příkazy"
date: 2026-03-26
author: "archos"
draft: false
categories: ['Návody', 'Arch Linux']
---

# Arch Linux – Základní příkazy

*Praktický průvodce pro začátečníky a mírně pokročilé uživatele*

## 1. Úvod

Arch Linux je minimalistická rolling-release distribuce – dostaneš čistý systém bez zbytečností a sám si ho postavíš podle sebe. Žádný GUI instalátor, žádné předinstalované haraburdí.

Proč znát příkazy? Protože na Archu neexistuje klikací záchranný kruh. Když se něco rozbije (a rozbije), terminal je jediná cesta ven. A taky je to prostě rychlejší než jakékoliv GUI.

## 2. Práce se systémem

### `uname -a` — informace o jádře

```bash
uname -a
# Linux mujpc 6.8.1-arch1-1 #1 SMP PREEMPT_DYNAMIC ...
```

Zobrazí jméno počítače, verzi kernelu a architekturu. Hodí se při hlášení bugů nebo kontrole kernelu po aktualizaci.

### `uptime` — jak dlouho běží systém

```bash
uptime
# 14:32:01 up 3 days, 2:14, 2 users, load average: 0.45, 0.60, 0.55
```

Ukazuje dobu běhu + průměrnou zátěž za 1, 5 a 15 minut.

### `htop` / `top` — sledování procesů

```bash
htop        # přehledná TUI verze (doporučeno)
top         # základní, vždy dostupný
```

`htop` umí kill procesu přímo z rozhraní – stiskni `F9`. Nainstaluj přes `sudo pacman -Syu htop`, pokud chybí.

## 3. Správa balíčků – pacman

Pacman je správce balíčků Arch Linuxu. Rychlý, jednoduchý, žádná magie.

### Aktualizace celého systému

```bash
sudo pacman -Syu
```

`-S` = synchronizace, `-y` = refresh databáze, `-u` = upgrade. Dělej pravidelně – Arch je rolling release.

### Instalace balíčku

```bash
sudo pacman -Syu firefox
sudo pacman -Syu git neovim htop   # více balíčků najednou
```

### Odstranění balíčku (včetně závislostí a config souborů)

```bash
sudo pacman -Rns firefox
```

`-R` = remove, `-n` = smaž config soubory, `-s` = smaž osiřelé závislosti. Vždy používej `-Rns`, ne jen `-R`.

### Hledání balíčku v repozitáři

```bash
pacman -Ss neovim
# extra/neovim 0.9.5-1
#     Vim-fork focused on extensibility and usability
```

### Hledání v nainstalovaných balíčcích

```bash
pacman -Qs neovim
# local/neovim 0.9.5-1
```

## 4. Práce se soubory a adresáři

### Orientace v systému

```bash
pwd             # kde jsem
ls -lah         # výpis adresáře (long, all, human-readable)
cd /etc/nginx   # přejít do adresáře
cd ..           # o úroveň výš
cd ~            # domovský adresář
```

### Kopírování, přesun, mazání

```bash
cp soubor.txt /tmp/soubor_backup.txt     # kopírování
cp -r slozka/ /tmp/slozka_backup/        # kopírování adresáře

mv soubor.txt novy_nazev.txt             # přejmenování
mv soubor.txt /home/user/dokumenty/      # přesun

rm soubor.txt                            # smazání souboru
rm -rf slozka/                           # smazání adresáře (POZOR, nevratné)
```

> 
⚠️ `rm -rf` se neptá. Dvakrát zkontroluj cestu.

### Vytváření adresářů

```bash
mkdir novy_adresar
mkdir -p projekty/web/css    # vytvoří celou cestu najednou
rmdir prazdny_adresar        # smaže jen prázdný adresář
```

### `tree` — stromové zobrazení

```bash
tree /etc/nginx
# Nainstaluj: sudo pacman -Syu tree
```

## 5. Práce s obsahem souborů

### Zobrazení obsahu

```bash
cat /etc/hostname                  # vypíše celý soubor
less /var/log/pacman.log           # stránkování, q = konec
bat /etc/fstab                     # zvýrazňování syntaxe (sudo pacman -Syu bat)
```

### Editory

```bash
nano /etc/hosts                    # jednoduchý, pro začátečníky
vim /etc/pacman.conf               # mocný, strmá učební křivka
nvim ~/.config/nvim/init.lua       # neovim – modernější vim
```

Základní vim survival kit:

```
i         → insert mode (psaní)
Esc       → zpět do normal mode
:w        → uložit
:q        → zavřít
:wq       → uložit a zavřít
:q!       → zavřít bez uložení
```

### `grep` — hledání v souborech

```bash
grep "error" /var/log/syslog                  # hledá "error" v souboru
grep -r "ServerName" /etc/nginx/              # rekurzivně v adresáři
grep -n "Port" /etc/ssh/sshd_config           # ukáže číslo řádku
journalctl | grep "failed"                    # filtrování výstupu
```

## 6. Oprávnění a vlastnictví

### `chmod` — práva souborů

```bash
chmod +x skript.sh               # přidej právo spuštění
chmod 644 soubor.txt             # rw-r--r--
chmod 755 /usr/local/bin/skript  # rwxr-xr-x (typické pro spustitelné soubory)
chmod -R 755 slozka/             # rekurzivně
```

Orientace v číslech:

```
4 = čtení (r)
2 = zápis (w)
1 = spuštění (x)

644 = vlastník rw, skupina r, ostatní r
755 = vlastník rwx, skupina rx, ostatní rx
```

### `chown` — změna vlastníka

```bash
chown user:group soubor.txt          # změna vlastníka i skupiny
chown -R www-data:www-data /var/www  # rekurzivně (typické pro web server)
```

## 7. Systémové služby – systemd

### Stav služby

```bash
systemctl status nginx
systemctl status sshd
```

### Start / stop / restart

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx     # znovu načte config bez restartu
```

### Povolení při startu systému

```bash
sudo systemctl enable nginx          # povolí autostart
sudo systemctl enable --now nginx    # povolí + hned spustí (doporučeno)
sudo systemctl disable nginx         # zakáže autostart
```

### Logy – journalctl

```bash
journalctl -xe                        # posledních X záznamů s kontextem chyb
journalctl -u nginx                   # logy konkrétní služby
journalctl -u nginx -f                # živý výstup (follow)
journalctl --since "1 hour ago"       # logy za poslední hodinu
journalctl -p err -b                  # jen chyby od posledního bootu
```

## 8. Síťové příkazy

### `ip a` — zobrazení síťových rozhraní

```bash
ip a                    # všechna rozhraní + IP adresy
ip a show eth0          # konkrétní rozhraní
ip r                    # routovací tabulka
```

### `ping` — test dostupnosti

```bash
ping archlinux.org
ping -c 4 8.8.8.8       # pošle jen 4 pakety
```

### `curl` — HTTP požadavky

```bash
curl https://archlinux.org                    # stáhni obsah stránky
curl -I https://archlinux.org                 # jen hlavičky (HTTP status atd.)
curl -O https://example.com/soubor.tar.gz     # stáhni soubor
curl -s https://api.ipify.org                 # zjisti svoji veřejnou IP
```

### `ss` — síťová spojení a porty

```bash
ss -tuln                  # všechny naslouchající TCP/UDP porty
ss -tulnp                 # + zobrazí proces
ss -s                     # souhrn statistik
```

## 9. Užitečné nástroje

### `yay` — správce AUR balíčků

AUR obsahuje tisíce balíčků mimo oficiální repozitáře.

```bash
# Instalace yay (jednorázově):
sudo pacman -Syu --needed git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay && makepkg -si

# Použití:
yay -Syu                        # aktualizace včetně AUR
yay -S visual-studio-code-bin   # instalace z AUR
yay -Ss spotify                 # hledání v AUR
```

### `rsync` — synchronizace a zálohy

```bash
rsync -avh ~/dokumenty/ /mnt/backup/dokumenty/         # lokální záloha
rsync -avh ~/dokumenty/ user@server:/backup/           # na vzdálený server
rsync -avh --delete ~/web/ user@server:/var/www/web/   # zrcadlení
rsync -n -avh ~/dokumenty/ /mnt/backup/                # dry run
```

`-a` = archivní mód, `-v` = verbose, `-h` = human-readable

### `du` a `df` — místo na disku

```bash
df -h                           # místo na všech připojených discích
df -h /home                     # konkrétní oddíl

du -sh ~/dokumenty              # velikost adresáře
du -sh /var/cache/pacman/pkg    # kolik zabírá cache pacmanu
du -h --max-depth=1 /var        # přehled velikostí podadresářů
```

## 10. Tipy na závěr

### Aliasy – zkratky pro časté příkazy

Přidej do `~/.bashrc` nebo `~/.zshrc`:

```bash
alias update='sudo pacman -Syu'
alias ll='ls -lah'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'
alias df='df -h'
alias du='du -h'
alias syslog='journalctl -xe'
```

Po úpravě:

```bash
source ~/.bashrc
```

### Historie příkazů

```bash
history                   # zobrazí historii
history | grep pacman     # hledej v historii
!!                        # zopakuj poslední příkaz
!ssh                      # zopakuj poslední příkaz začínající na "ssh"
```

Klávesové zkratky:

```
Ctrl+R   → interaktivní hledání v historii
         → piš část příkazu, Enter = spustí, Ctrl+R znovu = starší shoda
```

## Cheat Sheet

```
╔══════════════════════════════════════════════════════════════════╗
║                   ARCH LINUX — CHEAT SHEET                       ║
╠══════════════════╦═══════════════════════════════════════════════╣
║ SYSTÉM           ║ uname -a          → info o kernelu            ║
║                  ║ uptime            → jak dlouho běží           ║
║                  ║ htop              → procesy a zátěž           ║
╠══════════════════╬═══════════════════════════════════════════════╣
║ PACMAN           ║ pacman -Syu       → aktualizace               ║
║                  ║ pacman -Syu  → instalace                 ║
║                  ║ pacman -Rns  → odebrání                  ║
║                  ║ pacman -Ss   → hledání v repozitáři      ║
║                  ║ pacman -Qs   → hledání v instalovaných   ║
╠══════════════════╬═══════════════════════════════════════════════╣
║ SOUBORY          ║ ls -lah           → výpis adresáře            ║
║                  ║ cp -r src/ dst/   → kopírování                ║
║                  ║ mv src dst        → přesun / přejmenování     ║
║                  ║ rm -rf slozka/    → smazání (POZOR!)          ║
║                  ║ mkdir -p a/b/c    → vytvoření cesty           ║
╠══════════════════╬═══════════════════════════════════════════════╣
║ OBSAH SOUBORŮ    ║ cat soubor        → výpis                     ║
║                  ║ less soubor       → stránkování               ║
║                  ║ grep "text" soubor→ hledání                   ║
╠══════════════════╬═══════════════════════════════════════════════╣
║ SYSTEMD          ║ systemctl status  → stav služby               ║
║                  ║ systemctl enable  ║                           ║
║                  ║   --now      → povol + spusť             ║
║                  ║ journalctl -xe    → logy s chybami            ║
║                  ║ journalctl -u svc → logy služby               ║
╠══════════════════╬═══════════════════════════════════════════════╣
║ SÍŤ              ║ ip a              → síťová rozhraní           ║
║                  ║ ss -tuln          → otevřené porty            ║
║                  ║ curl -s URL       → HTTP požadavek            ║
╠══════════════════╬═══════════════════════════════════════════════╣
║ DISK             ║ df -h             → místo na discích          ║
║                  ║ du -sh /cesta     → velikost adresáře         ║
╠══════════════════╬═══════════════════════════════════════════════╣
║ HISTORY          ║ Ctrl+R            → hledání v historii        ║
║                  ║ !!                → zopakuj poslední příkaz   ║
╚══════════════════╩═══════════════════════════════════════════════╝
```