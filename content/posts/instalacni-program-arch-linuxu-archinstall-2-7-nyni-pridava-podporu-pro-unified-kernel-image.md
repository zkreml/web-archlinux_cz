---
title: "Instalační program Arch Linuxu, Archinstall 2.7, nyní přidává podporu pro Unified Kernel Image."
date: 2023-11-23
author: "archos"
draft: false
categories: ['rychlé zprávy']
---

Toto vydání rovněž zavádí funkci kontroly nových verzí archinstallu při spouštění instalačního programu Arch Linuxu.

Instalační program Arch Linuxu, archinstall, založený na menu, byl dnes aktualizován na verzi 2.7. Jedná se o hlavní vydání, které přináší řadu nových funkcí a opravuje mnoho chyb.

Archinstall 2.7 uvádí dvě důležité novinky: podporu pro Unified Kernel Image (UKI), což je jediný spustitelný soubor, který lze spouštět přímo z UEFI firmwaru, a možnost kontrolovat nové verze archinstallu při spouštění instalačního programu Arch Linuxu.

Kromě nové schopnosti kontroly verzí, nová verze Arch Linux instalačního programu také vylepšuje zprávy o chybách pro uživatele, rozšiřuje kontroly Mypy, přidává počáteční podporu hindštiny a přináší lepší dokumentaci s využitím CSV pro tabulky, reorganizaci definic parametrů a vylepšené rozložení.

Navíc archinstall 2.7 přidává balíček nvidia-dkms při instalaci proprietárního grafického ovladače NVIDIA, '--skip-ntp' parametr pro vyřešení chyby 'Čekání na dokončení synchronizace času (systemd-timesyncd.service)' během instalace, přidává možnost zpracování přerušení signálu a EOF u vstupních výzev a zjednodušuje dekódování SysCommand.

**Archinstall 2.7: Nové funkce a opravy chyb**

Dnes byla vydána aktualizace instalačního programu Arch Linux, archinstall, na verzi 2.7. Toto hlavní vydání přináší nové funkce a opravuje řadu chyb.

**Hlavní Novinky v Archinstall 2.7:**

- **Podpora pro Unified Kernel Image (UKI):** Jedná se o jediný spustitelný soubor, který lze spouštět přímo z UEFI firmwaru.

- **Kontrola nových verzí Archinstallu:** Tato funkce je nyní dostupná při spouštění instalačního programu Arch Linuxu.

Navíc nová verze instalačního programu vylepšuje reportování chyb uživatele, rozšiřuje kontrolu pomocí Mypy, přidává počáteční podporu hindštiny, a zavádí lepší dokumentaci s využitím CSV pro tabulky, reorganizaci definic parametrů a vylepšené rozložení.

Archinstall 2.7 dále zahrnuje balíček nvidia-dkms pro instalaci proprietárního grafického ovladače NVIDIA, parametr '--skip-ntp', který řeší chybu 'Čekání na dokončení synchronizace času (systemd-timesyncd.service)' během instalace, a přidává funkce pro zpracování přerušení signálu a EOF u vstupních výzev a zjednodušuje dekódování SysCommand.

**Opravy chyb:**

- Opravena chybějící informace pro předem nainstalovanou konfiguraci disku, rozložení klávesnice, nabídky časového pásma, inicializace textu instalace, reset v nabídce locales, náhled hesla, zarovnání konce GPT, zavaděč Limine a analýzu předběžně připojené konfigurace disku z konfiguračního souboru.

- Opraveny byly také proměnné MOUNT_POINT pro předem namontovanou konfiguraci disku, příkazový řádek EFISTUB a logické chyby v _fetch_lsblk_info() a encrypt() smyčkách.

- Toto vydání odstraňuje duplicity select_language() a select_kb_layout() a nadbytečné použití partprobe.

**Dostupnost a Nnasazení:** Archinstall 2.7 je k dispozici ke stažení na GitHubu a bude dostupný v repozitářích Arch Linuxu pro nezávislé distribuce s postupným vydáním na nové počítače. Archinstall 2.7 bude také výchozím instalačním programem v nadcházejícím snímku Arch Linux ISO pro prosinec 2023

**Tento článek byl původně publikován na** **[9to5linux](https://9to5linux.com/arch-linux-installer-archinstall-2-7-adds-support-for-unified-kernel-image)**