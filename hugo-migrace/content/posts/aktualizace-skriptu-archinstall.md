---
title: "Aktualizace skriptu archinstall"
date: 2022-04-30
author: "archos"
draft: false
tags: ['zprávy']
---

Instalační skript archinstall  byl aktualizován na verzi 2.4.1. Toto vydání přináší, řadu nových funkcí, vylepšení a také mnoho oprav chyb.

Největší novinkou vydání Archinstall 2.4.1 je zcela nový systém nabídek, který můžete vidět na snímku obrazovky. Zcela nový systém nabídek používá balík simple-term-menu Python, který vytváří jednoduché interaktivní nabídky na příkazovém řádku a je snadno přístupný. Kromě toho byl průvodce aktualizován, aby používal nový systém nabídek.

![](https://arch-linux.cz/wp-content/uploads/2022/04/archin-1024x585.webp)

Nový systém nabídek by měl instalaci **Arch Linuxu  **ještě více usnadnit. Mezi další nové funkce verze Archinstall 2.4.1 patří podpora komprese Btrfs při jeho výběru jako hlavního souborového systému,  stejně jako podpora pro bezproblémové načítání konfigurací a jejich ukládání. pomocí formátu „archinstall“.

Instalační skript Arch Linuxu nyní navíc umožňuje složitější rozvržení Btrfs,  přidává podporu pro instalaci správce oken Qtile během instalace a přidává profil pro správnou konfiguraci PipeWire.

Mechanismus rozdělení byl vylepšen také v této nové verzi Archinstall, která také přidává nový plugin pro provádění akcí po vytvoření na uživatelských profilech, nahrazuje textový editor Kate za KWrite v profilu KDE, přidává podporu psaní v celém instalačním skriptu, a zlepšuje `xorg`profil správně nastavit `amdgpu`moduly v hácích mkinitcpio.

Samozřejmě je v této aktualizaci zahrnuto mnoho dalších změn, které budou součástí příštího snímku Arch Linux ISO, jehož vydání je naplánováno na 1. května 2022. Pro více podrobností byste se měli podívat na [poznámky k vydání ](https://github.com/archlinux/archinstall/releases/tag/v2.4.1)na stránce projektu GitHub .

zdroj:  [9to5Linux](https://9to5linux.com/arch-linuxs-archinstall-gets-a-brand-new-menu-system-many-other-new-features)