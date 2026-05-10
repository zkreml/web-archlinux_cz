---
title: "Jak zálohovat pomocí  BorgBackup"
date: 2023-04-01
author: "archos"
draft: false
categories: ['Návody', 'Aplikace']
tags: ['borg', 'backup']
---

### Co je Borg

Borg  je open-source nástroj pro zálohování souborů a složek, který je k dispozici pro operační systémy Linux, macOS. Tento program je navržen tak, aby byl jednoduchý k použití, ale zároveň poskytoval robustní a spolehlivou zálohovací funkci pro ukládání důležitých dat.

Borg  používá jedinečnou technologii komprese dat, což umožňuje ukládat velké objemy dat v menších souborech, což zase znamená, že je možné ušetřit místo na disku. Další výhodou Borg Backupu je jeho rychlost - rychle zálohuje a obnovuje data, což je užitečné pro uživatele, kteří potřebují často měnit a ukládat data.

Borg poskytuje uživateli možnost zálohovat data do lokálního úložiště, jako jsou pevné disky, nebo do vzdáleného úložiště, jako jsou cloudové služby nebo FTP servery. Soubory a složky jsou zašifrovány pomocí AES-256, což zajišťuje bezpečnost a ochranu před neoprávněným přístupem.

V Borgu  lze nastavit pravidelné zálohování, což znamená, že se data automaticky zálohují v určených intervalech. Tato funkce je užitečná pro uživatele, kteří chtějí mít neustále aktuální zálohu svých dat.

Další výhodou BorgBackup  je  jednoduchost. Pro zálohování stačí pouze několik příkazů v příkazovém řádku, což umožňuje uživatelům rychle a snadno zálohovat a obnovovat svá data.

### Jak Borg funguje

Borg je to, čemu se říká „deduplikační zálohovací program“. Podobně jako u přírůstkových záloh jsou v následných zálohách archivována pouze data, která se skutečně změní na souborovém systému po provedení úplné zálohy, ale podobnosti jsou pouze koncepční. Borg funguje tak, že každý soubor rozdělí na části, které jsou identifikovány jejich hash součtem. Do „úložiště“ jsou přidány pouze bloky, které aplikace nerozpoznají. Tato technika deduplikace je skutečně účinná, protože mimo jiné nám umožňuje přesunout soubor nebo adresář, aniž by to bylo považováno za změnu, a proto vyžaduje další místo. Totéž platí pro časová razítka souborů. To, na čem skutečně záleží, jsou pouze části souborů, které se ukládají pouze jednou. V Linuxu Borg podporuje zachování všech standardních a rozšířených atributů souborového systému, jako jsou ACL a xattrs.

### Instalace Borga

Nejprve si musíte nainstalovat Borg. To lze provést pomocí správce balíčků, nebo si můžete stáhnout instalační soubory z oficiálních stránek.

```
sudo pacman -S borgbackup
```

### Vytvoření repozitáře

Předtím, než začnete zálohovat svá data, musíte vytvořit repozitář, kde se budou data ukládat. Můžete to udělat pomocí následujícího příkazu:

```
borg init -e repokey-blake2 /cesta/k/repozitari
```

Tento příkaz vytvoří nový Borg Backup repozitář v zadané cestě.

### Vytvoření zálohy

Nyní můžete vytvořit zálohu svých dat pomocí následujícího příkazu:

```
borg create /cesta/k/repozitari::jmeno-zalohy /cesta/k/slozkam-k-zalohovani
```

Tento příkaz vytvoří novou zálohu s názvem "jmeno-zalohy" a uloží ji do vašeho Borg Backup repozitáře. Data, která chcete zálohovat, musí být umístěna v adresáři uvedeném po druhém lomítku.

### Pravidelné zálohování

Pro pravidelné zálohování můžete použít nástroje jako Cron nebo Systemd timer. Pro příklad zálohování každý den v 2 ráno pomocí Cronu, můžete přidat následující řádek do svého Crontab souboru:

```
0 2 * * * /usr/bin/borg create /cesta/k/repozitari::`date +\%Y-\%m-\%d` /cesta/k/slozkam-k-zalohovani
```

Tento příkaz vytvoří zálohu každý den v 2 ráno s aktuálním datem jako název zálohy.

### Obnovení zálohy

Pokud potřebujete obnovit data ze zálohy, můžete to udělat pomocí následujícího příkazu:

```
borg extract /cesta/k/repozitari::jmeno-zalohy /cesta/k/kam-se-data-obnovi
```

### Základní příkazy

- `**borg init**`: Tento příkaz vytváří nový záložní repozitář.

- `**borg create**`: Tento příkaz vytváří novou zálohu vašich souborů nebo složek.

- **`borg list`:** Tento příkaz vypisuje seznam záloh v záložním repozitáři.

- `**borg info**`: Tento příkaz poskytuje informace o záložním repozitáři, jako je například jeho velikost a počet záloh.

- `**borg extract**`: Tento příkaz obnovuje soubory ze zálohy.

- `**borg delete**`: Tento příkaz odstraňuje zálohy z repozitáře.

- `**borg mount**`: Tento příkaz umožňuje přístup k obsahu záložního repozitáře jako ke složce, což umožňuje snadnější obnovu souborů.

- `**borg prune**`: Tento příkaz odstraňuje staré zálohy z repozitáře, aby se uvolnilo místo na disku

To jsou základní kroky pro použití Borg Backup pro zálohování vašich souborů a složek. Samozřejmě existuje mnoho dalších pokročilých funkcí, které můžete použít, abyste co nejlépe využili tohoto nástroje.