---
title: "CryFs - šifrování suborů"
date: 2022-07-31
author: "archos"
draft: false
categories: ['Aplikace']
tags: ['cryfs']
---

### CryFs

CryFS vytvořil Sebastian Messmer

[CryFS ](https://www.cryfs.org/)je bezplatný a otevřený cloudový šifrovací nástroj pro bezpečné ukládání souborů. Snadno se nastavuje, běží na pozadí a funguje dobře s jakoukoli populární cloudovou službou nevyjímaje **Dropbox **, **OneDrive**, **Nexctloud a iCloud**.

**CryFS **zajišťuje, že žádná data, včetně adresářové struktury, metadat a obsahu souborů, neopustí váš počítač v nezašifrovaném formátu.

**CryFS** šifruje na úrovni souborů, data pak ukládá do malých bloků (kontejnerů), jedná se o ideální řešení když nechceme šifrovat celé diskové oddíly či používat dedikované bloky

**CryFs** je jeden z nejlepších šifrovacích nástrojů v Linuxu.

### Vlastnosti CryFs

- Šifruje adresářovou strukturu vašich souborů tak, že zašifrovaná data nelze uhodnout spolu s obsahem souboru.

- Když je zašifrováno více dat, CryFS znovu nenahrává změny. Místo toho posílá malé změny, aby vám ušetřil místo na disku.

- Díky jednoduché a snadno pochopitelné struktuře příkazového řádku je přístupný běžnému uživateli.

- Šifruje metadata souborů

- Šifruje velikost souborů

- Nejsou zatím známy slabiny CryFS

- Opensource

### Instalace CryFs

Cryfs nainstalujem příkazem.

```
sudo pacman -S cryfs
```

### Nastavte šifrovaný adresář

Po instalaci můžete vytvořit šifrovaný adresář voláním **cryfs privat_data mount_data.** Adresáře můžete nazývat, jak chcete.

```
cryfs privat_data mount_data
```

Musíte  odpovědět na několik otázek, o konfiguraci vašeho šifrovaného adresáře. Na vše odpovíme yes.

CryFS vás také požádá o heslo, zadáme silné heslo a tím je vše nastaveno.

Soubory se upravuji v adresáři **mount_data**.

Zašifrovaný adresář odpojíme příkazem 

```
fusermount -u mount_data
```

Pro opětovné spuštění CryFs použijeme příkaz

```
cryfs privat_data mount_data
```

#### Důležité odkazy

- [Stránka projektu Cryfs](https://www.cryfs.org/)

- [Wiki Arch Linux ](https://man.archlinux.org/man/cryfs.1.en)