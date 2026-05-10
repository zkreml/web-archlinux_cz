---
title: "Pacman a AUR pomocníci"
date: 2022-02-19
author: "archos"
draft: false
categories: ['Návody']
tags: ['AUR', 'pacmam']
series: ['Arch Linux instalace']
---

V dalším díle seriálu  [Tondy Fischera ](https://github.com/raven2cz/tux) o [Arch LInuxu](https://arch-linux.cz/series/arch-linux-instalace/), se seznámíme se správci balíčku pro Arch Linux  a ukážeme si tripy a triky pro pacmana. Podíváme se na  AUR repozitář a  o používání  AUR pomocníků. Na video se můžete podívat na [Youtube autora ](https://www.youtube.com/watch?v=g60xHvIEyJ0), nebo našem [PeerTube kanále](https://peertube.arch-linux.cz/w/cBaNDGc6eYcksKXjqHck7p).

# [](https://github.com/raven2cz/tux/tree/main/210920-pacman-aur-helpers#pacman)Pacman

## [](https://github.com/raven2cz/tux/tree/main/210920-pacman-aur-helpers#první-krůčky)

## První krůčky

[Pacman-Arch-Wiki](https://wiki.archlinux.org/title/pacman) Správce balíků `pacman` je jednou z hlavních charakteristických vlastností **Arch Linuxu**. Kombinuje jednoduchý binární formát balíčku se snadno použitelným sestavovacím systémem (build system). Cílem pacmanu je umožnit snadnou správu balíčků, ať už jsou z oficiálních úložišť, nebo z vlastních sestavení uživatele.

Pacman udržuje systém aktuální synchronizací seznamů balíků s hlavním serverem. Tento model server/klient také umožňuje uživateli stahovat/instalovat balíčky jednoduchým příkazem, doplněný o všechny požadované závislosti.

Pacman je napsán v programovacím jazyce C a používá BSD tar formát pro balení.

```
sudo pacman -S awesome ## install package/meta-package
sudo pacman -Syu ## System update
sudo pacman -Syy ## sync database
pacman -Ss awesome ## search package with text 'gnome'
pacman -Qs awesome ## search installed packages
pacman -Si plasma-meta ## display extensive information
pacman -Qii awesome ## info + list of backup files
pacman -Qdt ## list packages no longer reqs (orphans)
sudo pacman -Sc ## clear packages in cached packages
sudo pacman -Scc ## all files in cache, strong aggresive, nothing leave in cache
sudo pacman -U /path/to/package/package_name-version.pkg.tar.zst #@ install local pckage, from AUR
sudo pacman -S --asdeps unzip ## install as dependency, can be removed as orphans
sudo pacman -Qe mc ## list version if it is explicitly installed
sudo pacman -D --asdeps unzip ## change the status to deps
sudo pacman -D --asexplicit unzip
sudo pacman -F pacman ## search files which are containing by package
sudo pacman --needed base-devel ## install if necessary
pactree awesome ## tree of depended packages
```

## [](https://github.com/raven2cz/tux/tree/main/210920-pacman-aur-helpers#pacman-configuration-etcpacmanconf)

## Pacman Configuration /etc/pacman.conf

Moje nastavení s barvami, přehlednou tabulkou stažení balíčků, opravodovým pacmanem a paralelním stahováním.

```
Color
CheckSpace
VerbosePkgLists
ILoveCandy
ParallelDownloads = 5
```

Bezpečnost a gpg podepisování: `SigLevel = Required DatabaseOptional` Pacman podporuje podpisy balíčků, které do balíků přidávají další vrstvu zabezpečení. Výchozí konfigurace, `SigLevel = Required DatabaseOptional`, umožňuje ověření podpisu pro všechny balíčky na globální úrovni.

Nikdy nepoužívejte `SigLevel = Never` (jen zcela v případě velké nouze, nebo člověka, kterého skutečně znáte a jeho závislost nelze obnovit kvůli nemoci například.)

## [](https://github.com/raven2cz/tux/tree/main/210920-pacman-aur-helpers#pacman-repositories-multilib-extra-community-a-úrověň-testing)

## Pacman Repositories multilib, extra, community a úrověň testing

Může se také stát, že úložiště obsahující balíček není ve vašem systému povoleno, např. Balíček může být v multilib úložišti, ale multilib není povolen ve vašem pacman.conf. Nutno povolit.

Můžete se stát i testerem pro Arch. Zapnout balíčky s `-testing`. Nutno pak ale updatovat celý systém, není jednoduchá změna! Pozor.

# [](https://github.com/raven2cz/tux/tree/main/210920-pacman-aur-helpers#aur-arch-user-repository)

# AUR (Arch User Repository)

**Arch User Repository (AUR)** je komunitní úložiště pro uživatele Arch. Obsahuje popisy balíků ( PKGBUILDs ), které vám umožňují sestavit balíček ze zdroje pomocí `makepkg` a poté jej nainstalovat pomocí pacman. AUR byla vytvořena za účelem organizace a sdílení nových balíčků z komunity a za účelem urychlení začlenění oblíbených balíčků do úložiště komunity.

Mnoho nových balíčků, které vstupují do oficiálních úložišť, začíná v AUR. V AUR mohou uživatelé přispívat svými vlastními sestavami balíků (PKGBUILDa související soubory). Komunita AUR má možnost hlasovat pro balíčky v AUR. Pokud se balíček stane dostatečně populárním - za předpokladu, že má kompatibilní licenci a dobrou techniku ​​balení - může být vložen do komunitního úložiště (přímo přístupného pacmanem nebo abs).

**Varování:** Balíčky AUR jsou uživatelsky vytvářený obsah. Tyto PKGBUILDjsou zcela neoficiální a nebyli důkladně prověřeni. Jakékoli použití poskytnutých souborů je na vaše vlastní riziko.

## [](https://github.com/raven2cz/tux/tree/main/210920-pacman-aur-helpers#yay-paru-aura-pomocníci-aur)

## Yay, Paru, Aura pomocníci AUR

- [JGuer/yay](https://github.com/Jguer/yay) - Yet Another Yogurt - An AUR Helper napsán v Go

- [Morganamilo/paru](https://github.com/Morganamilo/paru) - Paru AUR pomocník s mnoho features a minimální interakcí. Napsán Rust.

- [fosskers/aura](https://github.com/fosskers/aura) - Nadstandardní služby, zajímavé funkce, downgrades a zabezpečení upgrades a snapshots ovládání. Napsáno v Haskell.

### [](https://github.com/raven2cz/tux/tree/main/210920-pacman-aur-helpers#paru-instalace)

### Paru instalace

```
sudo pacman -S --needed base-devel
git clone https://aur.archlinux.org/paru-bin.git
cd paru-bin
makepkg -si
```

### [](https://github.com/raven2cz/tux/tree/main/210920-pacman-aur-helpers#paru-příklady-užití)

### Paru příklady užití

- `**paru **` - Interaktivně vyhledávejte a instalujte .

- `**paru**` - Alias ​​pro paru -Syu.

- `**paru -S **` - Nainstalujte si konkrétní balíček.

- **`paru -Sua` **- Upgradujte balíčky AUR.

- `**paru -Qua**` - Vytiskněte dostupné aktualizace AUR.

- `**paru -G **` - Stáhněte si PKGBUILD a související soubory z .

- **`paru -Gp ` **- Vytiskněte PKGBUILD z .

- **`paru -Gc ` **- Vytiskněte si komentáře AUR pro .

- **`paru --gendb` **- Vytvořte databázi devel pro sledování *-gitbalíčky. To je potřeba pouze tehdy, když zpočátku používáte paru.

- `**paru -Ui**` - Vytvořte a nainstalujte PKGBUILD do aktuálního adresáře.

### [](https://github.com/raven2cz/tux/tree/main/210920-pacman-aur-helpers#aura-instalace)

### Aura instalace

```
git clone https://aur.archlinux.org/aura-bin.git
cd aura-bin
makepkg
sudo pacman -U 
```

### [](https://github.com/raven2cz/tux/tree/main/210920-pacman-aur-helpers#aura-zajímavé-příkazy)

### Aura zajímavé příkazy

- `**aura -Pa**` - Analyzujte všechny místně nainstalované balíčky AUR.

- `**aura -O**` - Zobrazit osiřelé balíčky.

- `**aura -L**` - Zobrazit protokol Pacman.

- `**aura -Li **` - Zobrazit historii instalace / upgradu balíčku.

- **`aura -Cc ` **- Odstranit všechny kromě nejnovější nverze každého balíčku uloženého v mezipaměti.

- **`aura -C ` **- Downgrade balíčku.

- `**aura -Cv**` - Odstranit všechny /var/cache/aura/vcsmezipaměti

- `**aura -B**` - Uložte záznam JSON všech nainstalovaných balíčků.

- `**aura -Br**` - Obnovte uložený záznam. Podle potřeby se vrací zpět a odinstaluje.

- `**aura -Bc **` - Odstranit všechny kromě nejnovější nuložené státy.

- `**aura -Bl**` - Zobrazit všechny uložené názvy souborů stavu balíčku.

- `**aura -Au**` - Upgradujte všechny nainstalované balíčky AUR.

- **`aura -Akuax` - **Oblíbený autor (upgrady, odstranění makedeps, ukazuje rozdíly PKGBUILD, ukazuje postup)

- `**aura -As **` - Hledejte AUR pomocí regexu.

- `**aura -Ap **` - Zobrazit balíček PKGBUILD.

- `**aura -Ad **` - Seznam závislostí balíčku.

# [](https://github.com/raven2cz/tux/tree/main/210920-pacman-aur-helpers#důležité-odkazy)

https://www.youtube.com/watch?v=g60xHvIEyJ0

# Důležité odkazy

- [Youtube Channel TUX: Svět Linuxu](https://www.youtube.com/user/tondafischer/featured)

- [archlinux.org](https://archlinux.org/)

- [wiki.achlinux.org](https://wiki.archlinux.org/)

- [fishlive.org/blog](https://fishlive.org/en/blog-tech-art/arch)

- [github/raven2cz/tux](https://github.com/raven2cz/tux)

- [github/raven2cz/dotfiles](https://github.com/raven2cz/dotfiles)