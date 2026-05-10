---
title: "Jak nainstalovat  AUR pomocníka yay"
date: 2022-01-29
author: "archos"
draft: false
categories: ['Návody']
tags: ['AUR', 'yay']
---

**Upozornění: Instalace balíčků z AUR není podporována Arch Linuxem. Instalace z něj může způsobit selhání systému.**

### Co je  AUR

Arch User Repository (AUR) je komunitou řízené úložiště pro uživatele Arch Linuxu. Obsahuje popisy balíčků ( [PKGBUILDs](https://wiki.archlinux.org/title/PKGBUILD) ), které vám umožňují sestavit balíček ze zdrojového kódu pomocí [makepkg](https://wiki.archlinux.org/title/Makepkg) a poté jej nainstalovat přes [pacman](https://wiki.archlinux.org/title/Pacman#Additional_commands) . AUR byl vytvořen, aby organizoval a sdílel nové balíčky z komunity a pomohl urychlit začlenění oblíbených balíčků do [komunitního úložiště](https://wiki.archlinux.org/title/Community_repository) .

Velký počet nových balíčků, které vstupují do oficiálních repozitářů, začíná v AUR. V AUR mohou uživatelé přispívat vlastním sestavením balíčků (PKGBUILD a související soubory).

Komunita AUR má možnost hlasovat pro balíčky v AUR. Pokud se balíček stane dostatečně populárním – za předpokladu, že má kompatibilní licenci a dobrou balicí techniku ​​– může být vložen do komunitního úložiště.

Na rozdíl od balíčků v repozitáři Archu jsou balíčky AUR spravovány uživateli Archu a většina to dělá jako koníčka vedle svého běžného života. Aktualizace balíčků proto nejsou rozsáhle testovány a mohou způsobit potíže nereagující aplikací nebo dokonce způsobit poškození systému, takže jejich použití je na vaši vlastní odpovědnost.

### **Co je yay**

Yay je zkratka pro 'Yet Another Yogurt'. Technicky jde o [pacmana](https://wiki.archlinux.org/index.php/pacman) a pomocníka AUR napsaný v [programovacích jazycích Go](https://golang.org/) . Je to nejpopulárnější [Arch User Repository (AUR)](https://wiki.archlinux.org/index.php/Arch_User_Repository) pomocník. S Yay můžete využít výhody obrovského Arch User Repository balíčků a snadno zkompilovat a nainstalovat  software.

V podstatě automatizuje mnoho úloh správy balíčků, jako je vyhledávání, řeší závislosti za běhu, kompiluje a sestavuje balíčky a samozřejmě publikuje vaše vlastní balíčky pro AUR.

### Nainstalujte yay v Arch Linuxu

### Požadavky

Tyto kroky vyžadují [base-devel](https://aur.archlinux.org/packages/meta-group-base-devel/) ke kompilaci a instalaci balíček Otevřete terminál a spusťte níže uvedené příkazy. Po zobrazení výzvy zadejte heslo správce.

```
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

## Instalace balíčků

Chcete-li nainstalovat balíčky pomocí yay, můžete použít tento příkaz.

```
yay -S název_balíčku
```

Poté uvidíte očíslovaný seznam názvů balíčků v nainstalovaných úložištích vašeho systému. Jednoduše zadejte číslo verze balíčku, kterou chcete nainstalovat, a yay ji nainstaluje do vašeho systému.

Balíčky můžete také vyhledávat jednoduchým zadáním:

```
yay název_balíčku
```

Pokud chcete další informace o balíčku, můžete zadat:

```
yay -Si název_balíčku
```

Yay může také aktualizovat balíčky Pacman a AUR najednou pomocí tohoto příkazu:

```
yay -Syu
```