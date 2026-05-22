---
title: "EndeavourOS – podrobný průvodce distribucí postavenou na Arch Linuxu"
date: 2026-05-22
draft: false
description: "Kompletní průvodce EndeavourOS – historie, instalace, správa balíčků, srovnání s Archem a tipy pro každodenní používání."
tags: ["arch-linux", "endeavouros", "linux", "distribuce"]
categories: ["Distribuce"]
image: "krimkerre_3_endy.jpg"
---

{{< figure src="krimkerre_3_endy.jpg" alt="EndeavourOS" >}}

EndeavourOS patří mezi nejoblíbenější distribuce založené na Arch Linuxu. Nabízí přístupný způsob, jak se dostat k čistému Arch zážitku bez nutnosti ruční instalace přes příkazový řádek. V tomto článku se podíváme na vše podstatné – od historie přes instalaci až po každodenní používání a porovnání s čistým Archem.

---

## Co je EndeavourOS?

EndeavourOS je komunitní rolling-release distribuce založená přímo na Arch Linuxu. Na rozdíl od Manjara nebo jiných Arch derivátů se snaží zůstat co nejblíže vanilkovému Archu – neudržuje vlastní repozitáře s odloženými balíčky, nepřepisuje systémové nástroje a nepřidává zbytečné vrstvy abstrakce.

Hlavní myšlenka je jednoduchá: vzít Arch Linux, přidat grafický instalátor Calamares a nabídnout uživateli téměř čistý systém připravený k vlastní konfiguraci. Zbytek je na vás.

---

## Historie a vznik

EndeavourOS vznikl v červenci 2019 jako duchovní nástupce zaniklé distribuce Antergos. Když vývojáři Antergosu v květnu 2019 oznámili ukončení vývoje, moderátor komunitního fóra Bryan Poerwoatmodjo přišel s nápadem zachovat alespoň komunitu na novém fóru. Během několika dní se k němu přidali další moderátoři – Johannes Kamprad, Fernando Omiechuk Frozi a Manuel – a plán se rozrostl z pouhého fóra na vznik úplně nové distribuce.

Důležité je, že EndeavourOS nikdy nebyl klon Antergosu. Vývojáři vědomě zvolili vlastní cestu – jiný vizuální styl, jiný přístup k instalaci a především důraz na komunitu jako hlavní devízu projektu. Antergos používal vlastní instalátor Cnchi, který se ukázal jako problematický mimo jeho ekosystém. EndeavourOS proto přešel na Calamares, univerzální grafický instalátor používaný řadou dalších distribucí.

První verze vyšla 15. července 2019 s offline instalátorem a upraveným prostředím Xfce. Online instalátor přibyl v prosinci téhož roku.

---

## Aktuální stav (2026)

V březnu 2026 vyšla verze **Titan** (2026.03.06) s jádrem Linux 6.19, KDE Plasma 6.6, Mesa 26.0.1 a instalátorem Calamares 26.03. V květnu 2026 ji následovala aktualizace **Titan Neo** s jádrem 6.19.14 a KDE Plasma 6.6.4.

Důležité změny v aktuální verzi:

- **NVIDIA Open kernel moduly** – od řady R590 se EndeavourOS přesunul na otevřené NVIDIA moduly, podpora pouze pro GPU řady GTX 1600 / RTX 20 (Turing) a novější
- **eos-hwtool** – nový nástroj pro správu hardwaru
- **Vylepšený mirror ranking** – optimalizovaný seznam zrcadel i při offline instalaci
- **Automatická instalace Vulkan ovladačů** a balíčků pro hardwarovou akceleraci videa
- **dracut místo mkinitcpio** – EndeavourOS používá dracut pro generování initramfs, což je jeden z klíčových rozdílů oproti čistému Archu

---

## Instalace

### Systémové požadavky

| Parametr | Minimum |
|----------|---------|
| Procesor | 64-bit dvoujádrový Intel/AMD |
| RAM | 4 GB |
| Disk | 15 GB volného místa |
| Firmware | UEFI (doporučeno) |

### Stažení a ověření ISO

ISO stáhnete z [endeavouros.com](https://endeavouros.com). Velikost ISO je přibližně 3,4 GB.

```bash
# ověření integrity
sha512sum -c EndeavourOS_Titan-Neo-2026.04.27.iso.sha512

# ověření GPG podpisu
gpg --recv-keys CDF595A1
gpg --verify EndeavourOS_Titan-Neo-2026.04.27.iso.sig
```

### Vytvoření bootovacího USB

```bash
# pomocí dd
sudo dd if=EndeavourOS_Titan-Neo-2026.04.27.iso of=/dev/sdX bs=4M status=progress oflag=sync

# nebo pomocí ventoy
# https://www.ventoy.net
```

### Dva režimy instalace

EndeavourOS nabízí dva způsoby instalace:

**Offline instalace** – nevyžaduje internet. Nainstaluje KDE Plasma v konfiguraci totožné s live prostředím. Ideální pro rychlý start nebo prostředí bez připojení.

**Online instalace (netinstall)** – vyžaduje internet. Stahuje balíčky přímo z repozitářů, takže máte zaručeně nejnovější verze. Hlavní výhodou je výběr desktopového prostředí přímo během instalace.

### Dostupná desktopová prostředí (online instalace)

- **KDE Plasma** – výchozí, moderní a vysoce konfigurovatelné
- **GNOME** – minimalistické, dotykové ovládání
- **Xfce** – lehké, stabilní, nízká spotřeba zdrojů
- **Cinnamon** – tradiční rozložení, vhodné pro přechod z Windows
- **MATE** – klasický desktop, nenáročný
- **Budgie** – elegantní a jednoduchý
- **LXQt** – extrémně lehké prostředí
- **LXDE** – starší, ale velmi nenáročné
- **i3** – tiling window manager pro pokročilé

Pokud se rozhodujete: pro úplné začátečníky je vhodné KDE Plasma nebo Cinnamon. Pro slabší hardware LXQt nebo Xfce. Pro pokročilé uživatele i3.

### Průběh instalace

Instalátor Calamares vás provede těmito kroky:

1. **Jazyk a lokalizace** – výběr jazyka, časové zóny a rozložení klávesnice
2. **Oddíly disku** – automatické rozdělení, ruční úprava nebo využití celého disku (podpora LUKS2 šifrování)
3. **Uživatel** – nastavení jména, hesla a hostname
4. **Bootloader** – systemd-boot nebo GRUB (výchozí je systemd-boot na UEFI systémech)
5. **Desktop** – výběr prostředí (pouze online režim)
6. **Instalace** – Calamares zobrazuje průběh instalace včetně terminálového výstupu

Po restartu vás přivítá **EndeavourOS Welcome App** – aplikace s odkazy na dokumentaci, aktualizaci systému a základní konfiguraci.

---

## Po instalaci – první kroky

### Aktualizace systému

```bash
# vždy jako první krok po instalaci
sudo pacman -Syu
```

### Instalace AUR helperu

EndeavourOS ve výchozím stavu dodává `yay` jako AUR helper:

```bash
# pokud by chyběl
sudo pacman -Syu git base-devel
git clone https://aur.archlinux.org/yay-bin.git
cd yay-bin
makepkg -si
```

### Základní balíčky

```bash
# editory
sudo pacman -Syu vim neovim nano

# síťové nástroje
sudo pacman -Syu wget curl rsync openssh

# systémové info
sudo pacman -Syu htop btop fastfetch

# multimédia
sudo pacman -Syu vlc firefox thunderbird

# fonty
sudo pacman -Syu noto-fonts noto-fonts-cjk ttf-liberation
```

### Nastavení firewallu

```bash
sudo pacman -Syu firewalld
sudo systemctl enable --now firewalld
```

### Povolení TRIM pro SSD

```bash
sudo systemctl enable --now fstrim.timer
```

---

## Správa balíčků

EndeavourOS používá `pacman` jako hlavní správce balíčků – stejně jako čistý Arch. Žádný grafický správce balíčků není předinstalován záměrně, aby se uživatelé učili pracovat s terminálem.

### Základní příkazy pacmanu

```bash
# aktualizace systému
sudo pacman -Syu

# instalace balíčku (vždy s -Syu!)
sudo pacman -Syu nazev-balicku

# vyhledání balíčku
pacman -Ss klicove-slovo

# informace o balíčku
pacman -Si nazev-balicku

# seznam nainstalovaných balíčků
pacman -Q

# odstranění balíčku včetně závislostí
sudo pacman -Rns nazev-balicku

# vyčištění cache
sudo pacman -Sc
```

### AUR (Arch User Repository)

AUR je komunitní repozitář se zdrojovými PKGBUILD soubory. EndeavourOS ho podporuje standardně přes `yay`:

```bash
# vyhledání v AUR
yay -Ss nazev

# instalace z AUR
yay -Syu nazev-balicku
```

---

## EndeavourOS vs. čistý Arch Linux

| Vlastnost | EndeavourOS | Arch Linux |
|-----------|-------------|------------|
| Instalace | Grafický Calamares | Ruční (archinstall skript) |
| Initramfs | dracut | mkinitcpio |
| AUR helper | yay předinstalován | Nutno doinstalovat |
| Repozitáře | Arch + malý EOS repo | Pouze Arch |
| Výchozí desktop | KDE Plasma | Žádný |
| Welcome App | Ano | Ne |
| Kernel | Stejný jako Arch | Stejný |
| Balíčky | Stejné jako Arch | Stejné |
| Rolling release | Ano | Ano |
| Komunita | Vlastní fórum + Telegram | Arch Wiki + fórum |

EndeavourOS přidává oproti čistému Archu jen minimum:

- **endeavouros-keyring** a **endeavouros-mirrorlist** – klíče a zrcadla pro EOS repozitář
- **eos-hooks** – hooky pro pacman
- **eos-hwtool** – detekce a konfigurace hardwaru
- **eos-apps-info** – Welcome App
- Několik dalších menších utilit specifických pro EOS

Důležité: po aktualizaci systému přes `pacman -Syu` dostáváte úplně stejné balíčky jako uživatelé čistého Archu.

---

## EndeavourOS vs. Manjaro

Časté srovnání, ale přístupy jsou zásadně odlišné:

| Vlastnost | EndeavourOS | Manjaro |
|-----------|-------------|---------|
| Repozitáře | Přímo Arch | Vlastní (zpožděné) |
| Balíčky | Aktuální jako Arch | Zpožděné o týdny |
| AUR kompatibilita | Plná | Může nastat nesoulad verzí |
| Předinstalovaný software | Minimum | Hodně |
| Přístup | Terminálově orientovaný | GUI orientovaný |
| Cílová skupina | Mírně pokročilí | Začátečníci |

EndeavourOS je blíže čistému Archu. Manjaro je samostatnější distribuce, která se od Archu více vzdaluje.

---

## Vlastní nástroje EndeavourOS

### Welcome App

Grafická aplikace, která se spustí po prvním přihlášení. Obsahuje:

- Odkazy na dokumentaci a fórum
- Aktualizaci systému
- Přidání/odebrání desktopových prostředí
- Instalaci dalších nástrojů a ovladačů

### eos-hwtool

Nový nástroj zavedený ve verzi Titan pro detekci hardwaru a automatickou instalaci odpovídajících ovladačů.

### reflector-simple

GUI nadstavba nad `reflector` pro výběr nejrychlejších pacman zrcadel.

---

## Tipy pro každodenní používání

### Automatické zálohy seznamu balíčků

```bash
# uložení seznamu explicitně instalovaných balíčků
pacman -Qqe > ~/balicky-seznam.txt

# obnovení ze seznamu
sudo pacman -Syu - < ~/balicky-seznam.txt
```

### Správa služeb

```bash
# seznam aktivních služeb
systemctl list-units --type=service --state=running

# povolení služby
sudo systemctl enable --now nazev.service

# zobrazení logů
journalctl -u nazev.service -f
```

### Timeshift nebo Snapper pro snapshoty

```bash
# Timeshift pro ext4/btrfs
yay -Syu timeshift

# nebo Snapper pro btrfs
sudo pacman -Syu snapper
```

### Údržba systému

```bash
# kontrola neúspěšných služeb
systemctl --failed

# kontrola logů za chyby
journalctl -p 3 -b

# vyčištění pacman cache (ponechá poslední 3 verze)
sudo paccache -r

# odebrání osiřelých balíčků
sudo pacman -Rns $(pacman -Qdtq)
```

---

## Komunita a podpora

Komunita je považována za jednu z nejvstřícnějších v linuxovém světě. Vývojáři od začátku kladli důraz na přátelské prostředí, kde se začátečníci nebojí ptát.

**Hlavní zdroje:**

- **Fórum:** [forum.endeavouros.com](https://forum.endeavouros.com) – primární místo pro dotazy a diskuze
- **Telegram:** oficiální skupina pro rychlou komunikaci
- **Arch Wiki:** [wiki.archlinux.org](https://wiki.archlinux.org) – protože EndeavourOS je de facto Arch, veškerá dokumentace z Arch Wiki platí i zde
- **Web:** [endeavouros.com](https://endeavouros.com) – novinky, návody a stahování

---

## Pro koho je EndeavourOS vhodný?

**Ano, pokud:**

- Chcete Arch Linux bez bolestivé ruční instalace
- Chcete mít aktuální systém s rolling release
- Chcete se učit Linux a terminál, ale s bezpečnostní sítí grafického instalátoru
- Máte alespoň základní znalosti Linuxu (nebo ochotu se učit)
- Chcete minimální systém, který si sami nakonfigurujete

**Spíše ne, pokud:**

- Hledáte „nainstaluj a zapomeň" distribuci – zvažte Linux Mint nebo Fedora
- Potřebujete dlouhodobou podporu (LTS) – zvažte Ubuntu LTS nebo Debian Stable
- Nechcete se vůbec dotýkat terminálu – EndeavourOS je záměrně terminálově orientovaný

---

## Závěr

EndeavourOS je skvělá brána do světa Arch Linuxu. Neodstraňuje složitost Archu – jen vám usnadní ten nejtěžší krok: instalaci. Od momentu, kdy se přihlásíte do systému, pracujete s prakticky čistým Archem a máte plnou kontrolu nad tím, jak si systém přizpůsobíte.

Silná a vstřícná komunita, pravidelné aktualizace ISO a minimalistický přístup bez zbytečného bloatware dělají z EndeavourOS jednu z nejlepších voleb pro uživatele, kteří chtějí Arch bez kompromisů, ale s komfortnějším startem.

---

**Užitečné odkazy:**

- [EndeavourOS – oficiální web](https://endeavouros.com)
- [EndeavourOS fórum](https://forum.endeavouros.com)
- [EndeavourOS na Telegramu](https://t.me/Endeavouros)
- [Arch Wiki](https://wiki.archlinux.org)
- [EndeavourOS na GitHubu](https://github.com/endeavouros-team)
