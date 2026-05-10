---
title: "Desktopový klient pro Borg Backup Vorta"
date: 2023-04-09
author: "archos"
draft: false
categories: ['Aplikace návody']
series: ['Zálohování v Linuxu']
---

### Co je Vorta

Vorta je open-source aplikace pro zálohování dat v Linuxu. Jedním z hlavních důvodů, proč se Vorta stala oblíbenou mezi uživateli Linuxu, je její snadná instalace a použití. Vorta je k dispozici v mnoha distribucích Linuxu, jako je například Ubuntu, Fedora, Debian, Arch Linux a další. Po instalaci aplikace se uživatelé mohou snadno připojit k existujícímu účtu Borg Backup nebo si vytvořit nový účet a začít vytvářet zálohy.

Vorta má také mnoho užitečných funkcí, jako je například možnost plánovat pravidelné zálohování, možnost vytvářet zálohy z různých zdrojů dat, jako jsou například složky, soubory, nebo celé disky, a možnost šifrování záloh pro zajištění bezpečnosti dat.

Dále je také možné vytvářet zálohy na vzdálených serverech.

![](https://arch-linux.cz/wp-content/uploads/2023/04/ArcoLinux_2023-04-09_10-59-30-1024x575.png)

### Výhody

- **Šifrované, deduplikované a komprimované zálohy** využívající [Borg](https://borgbackup.readthedocs.io) jako backend.

- **Žádné uzamčení dodavatel**é – zálohujte na místní disky, svůj vlastní server nebo [BorgBase](https://www.borgbase.com) , hostingovou službu pro Borgské zálohy.

-  **Open source** – zdarma k použití, úpravě, vylepšení a auditu. 

- **Flexibilní profily** pro seskupování zdrojových složek, cílů zálohování a plánů. 

- **Jedno místo** pro zobrazení všech archivů k určitému okamžiku a obnovení jednotlivých souborů.

### Instalace

K instalaci použijte [balíček AUR](https://aur.archlinux.org/packages/vorta/)

```
yay -S vorta
```

### Nastavení Vorty pro místní zálohy

Po spuštění Vorty byste měli vidět nové okno nastavení.

![](https://arch-linux.cz/wp-content/uploads/2023/04/vorta_uvod-1024x575.png)

### Nastavení místního úložiště

Klikněte na **Úložiště** rozevírací nabídku **a vyberte možnost Inicializovat nové úložiště** . Po kliknutí by se mělo objevit nové okno.

![](https://arch-linux.cz/wp-content/uploads/2023/04/nastaveni_repo.png)

Klikněte na ![](https://vorta.borgbase.com/assets/images/vorta/local3.png)ikonu a vyberte adresář, ve kterém chcete inicializovat své nové úložiště Borg. Zadejte vámi vybranou přístupovou frázi pro úložiště. **Ujistěte se a uložte své přístupové heslo na bezpečném místě!** Když jste si jisti, že jsou všechny informace, které jste zadali, správné, stiskněte **Přidat** .

### Přidejte složky k zálohování

S nastavením úložiště můžete nyní přidat nějaké záložní složky a vytvořit svou první zálohu. Přejděte na kartu Zdroje a přidejte nějaké složky nebo výjimky.

![](https://arch-linux.cz/wp-content/uploads/2023/04/pridani_slozek-1024x575.png)

Poté stiskněte **Spustit zálohování** a proveďte první zálohu. Po každé úspěšné záloze (nebo snímku) bude na **Snímek** záložku přidán nový řádek. Tam můžete také připojit snímek a obnovit soubory.

### Obnovte soubory ze zálohy

Chcete-li začít s obnovou snímku souborů, spusťte Vorta a klikněte na **kartu Archivy** .

![](https://arch-linux.cz/wp-content/uploads/2023/04/obnova_vorta1-1024x572.png)

Existují dva způsoby, jak obnovit soubory pomocí Vorta, *Extrahování* a *Připojení* . Oba dosahují stejného cíle, ale jeden může být výhodnější než druhý v závislosti na situaci.

#### Extrahování z archivu

Po otevření **karty Archivy** ve Vortě a výběru snímku, ze kterého chcete obnovit, klikněte na **tlačítko Rozbalit** v boční části a  zobrazí se následující okno.

![](https://arch-linux.cz/wp-content/uploads/2023/04/vorta_2.png)

V dalším okně, které se zobrazí, se zobrazí dotaz na *Bod extrahování* nebo umístění, do kterého chcete zálohu extrahovat. Vyberte umístění a pokračujte.

#### Připojení zálohy

Po otevření **karty Archivy** ve Vortě a výběru snímku, ze kterého chcete obnovit, klikněte na **tlačítko Připojit** ve spodní části. Vyberte adresář pro připojení, bude to adresář, který Vorta použije, aby vám umožnil přístup k této záloze, jako by byla stále ve vašem souborovém systému. Ujistěte se, že se jedná o prázdný adresář.

Po dokončení obnovy souborů zavřete všechna aktivní okna a stiskněte **tlačítko Odpojit** .

#### Důležité odkazy:

- **[Dokumentace Borg](https://borgbackup.readthedocs.io/en/stable/)**

- **[Hosting pro Borg](https://www.borgbase.com/)**