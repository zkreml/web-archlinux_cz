---
title: "Správce hesel Bitwarden"
date: 2022-12-02
author: "archos"
draft: false
categories: ['Návody', 'Aplikace']
tags: ['bitwarden']
---

### Co je Bitwarden

[Bitwarden](https://bitwarden.archoslinux.cz/#/login) je všestranný správce hesel s otevřeným zdrojovým kódem, který může být použit nejen jednotlivci k ukládání jejich kritických a důležitých informací, ale také jej mohou nasadit podniky na všech úrovních. [Bitwarden](https://bitwarden.archoslinux.cz/#/login) lze stáhnout na mobilní telefony se systémem iOS i Android a poskytuje spoustu rozšíření prohlížeče pro automatické vyplňování hesel. Je to jeden z nejlepších open source správců hesel.

Nejen to, [Bitwarden ](https://bitwarden.archoslinux.cz/#/login)také poskytuje webové a desktopové aplikace spolu s rozhraním příkazového řádku, díky kterému je jedním z nejlepších multiplatformních správců hesel, které pokrývají všechny klientské aplikace. Můžete jej snadno použít jako desktopovou aplikaci pro macOS, Linux a Windows. 

Pokud jde o ochranu informací uložených na [Bitwarden](https://bitwarden.archoslinux.cz/#/login), správce hesel používá 256bitový šifrovací protokol AES, který znemožňuje hackování a vloupání. Kromě toho jsou všechny informace uloženy v zašifrovaném trezoru, ke kterému má vlastník přístup pouze prostřednictvím hlavního klíče.

### Vytvořte si účet Bitwarden

Na námi hostovaný [ Bitwarden](https://bitwarden.archoslinux.cz/#/login) se můžete registrovat [zde](https://bitwarden.archoslinux.cz/#/register)

Na obrazovce Vytvořit účet vyplňte všechna pole (Nápověda k hlavnímu heslu je volitelná) a vyberte **Odeslat** .

![](https://arch-linux.cz/wp-content/uploads/2022/12/Vytvorit_ucet.png)

Vytvořte si účet

Jakmile si vytvoříte svůj účet, požádejte Bitwarden, aby vám poslal ověřovací e-mail tak, že se přihlásíte do svého [webového trezoru](https://bitwarden.archoslinux.cz/#/login) a vyberete tlačítko **Ověřit e-mail** .

### Začněte s Web Vault

Webový trezor [Bitwarden](https://bitwarden.archoslinux.cz/#/login) poskytuje osobním uživatelům a organizacím nejbohatší prostředí [Bitwarden](https://bitwarden.archoslinux.cz/#/login). Mnoho důležitých funkcí, jako je nastavení dvoufázového přihlášení nebo správa organizace , musí být prováděno z webového trezoru.

![](https://arch-linux.cz/wp-content/uploads/2022/12/Snimek-obrazovky-z-2022-12-02-12-18-47-1024x571.png)

Když se poprvé přihlásíte do svého webového trezoru, dostanete se do **zobrazení ** **Trezoru**. V tomto prostoru budou uvedeny všechny položky trezoru, včetně přihlašovacích údajů, karet, identit a bezpečnostních poznámek .

Na předchozím snímku obrazovky se v **zobrazení Trezor**u zobrazuje **Všechny položky** v **mém trezoru** . Uživatelé organizací zde budou mít uvedeny další trezory. Pomocí **sloupce Filtry** můžete uspořádat úschovnu do **Oblíbených** a **Složek** .

Začněme nastavením nové složky a přidáním nového přihlašovacího jména:

Chcete-li vytvořit složku:

- Vyberte ikonu  **Přidat** vedle části Složky ve sloupci Filtry.

- Zadejte název (např. `Sociální sítě`) pro vaši složku a vyberte **Uložit** .

![](https://arch-linux.cz/wp-content/uploads/2022/12/vytvoreni-slozky-1024x571.png)*Vytvoření složky*

### Přidejte položku přihlášení

Chcete-li přidat novou položku přihlášení:

- Vyberte tlačítko  **Přidat položku** .

- Z rozevírací nabídky vyberte možnost **Přihlásit** (pokud místo toho přidáváte kartu, identitu nebo zabezpečenou poznámku, vyberte tuto možnost).

- Zadejte **název** položky. Názvy vám pomohou snadno identifikovat položky ve vašem trezoru, proto dejte této položce rozpoznatelnou (např. `Mastodon Arch Linux`).

- Zadejte své **uživatelské jméno** a **heslo** . Prozatím zadejte své stávající heslo. vám jej pomůžeme nahradit silnějším heslem později.

- Do pole **URI 1** zadejte adresu URL webové stránky (např. `https://mastodon.arch-linux.cz`). Pokud nevíte, jakou adresu URL použít, přejděte na přihlašovací obrazovku webové stránky a zkopírujte ji z adresního řádku.

- Z rozevíracího seznamu **Složka** vyberte název složky, do které chcete přidat tuto položku (např `Sociální sítě`složku, kterou jsme vytvořili dříve). Chcete -li tuto položku přidat mezi oblíbené, vyberte ikonu hvezdičky.

- Klepnutím na **tlačítko Uložit** dokončíte přidávání této položky.      

![](https://arch-linux.cz/wp-content/uploads/2022/12/pridat-polozku.png)*Přidání položky*

### Vygenerujte si silné heslo

Nyní, když je ve vašem trezoru uloženo nové přihlášení, vylepšete jeho zabezpečení nahrazením stávajícího hesla silnějším:

- Ve svém trezoru vyberte položku, kterou chcete zabezpečit.

- Na nové kartě nebo okně otevřete odpovídající webovou stránku a přihlaste se ke svému účtu. 

- Na tomto webu přejděte do oblasti, kde můžete **změnit heslo** . Obvykle to najdete v **části Váš účet** , **Zabezpečení** , **Nastavení** přihlášení nebo **Nastavení přihlášení** .

- Většina webových stránek vyžaduje nejprve zadání **aktuálního hesla** . Vraťte se do svého trezoru a vyberte ikonu **Kopírovat** vedle **pole Heslo** . Poté se vraťte na web a vložte jej do pole **Aktuální heslo** . Možná si staré heslo zapamatujete, ale je dobré si zvyknout heslo zkopírovat a vložit. Takto se budete přihlašovat, jakmile bude vaše heslo nahrazeno silnějším.

- Vraťte se do svého trezoru a klikněte na ikonu  **Generovat** vedle **pole Heslo** . Budete dotázáni, zda chcete přepsat aktuální heslo, takže **výběrem Ano .** pokračujte Toto nahradí vaše **heslo** náhodně vygenerovaným silným heslem. Přesun z hesla jako `1234`na `x*wNvUpKagnv^5q9m74X` může zastavit hackera.

- Zkopírujte své nové heslo pomocí stejné ikony  **Kopírovat** , kterou jste použili dříve, a vyberte tlačítko **Uložit** .

- Vraťte se na druhý web a vložte své silné heslo do **Nové heslo** a **Potvrdit nové heslo .**

- Jakmile **uložíte** změnu hesla, máte nové heslo hotovo!

```
**tip**:  Nedělejte si starosti s přepsáním svého stávajícího hesla! Pokud se něco pokazí, Bitwarden udržuje **historii hesel** posledních pěti hesel pro každé přihlášení: ![View Password History]()
```

![](https://arch-linux.cz/wp-content/uploads/2022/12/Historie-hesel.png)*Historie hesel*

### Zabezpečte svůj trezor

Nyní, když je váš trezor plný dat, pojďme podniknout kroky k jeho ochraně nastavením dvoufázového přihlášení. Dvoufázové přihlášení vyžaduje, abyste při přihlašování ověřili svou identitu pomocí dalšího tokenu, který je obvykle načten z jiného zařízení.

Existuje mnoho dostupných metod pro dvoufázové přihlášení, ale doporučenou metodou pro bezplatný účet Bitwarden je použití aplikace pro ověřování mobilních zařízení, jako je [Authy](https://authy.com/) :

- Stáhněte si Authy do svého mobilního zařízení.

- Ve svém webovém trezoru vyberte ikonu profilu a **účtu :** **vyberte Nastavení** z rozbalovací nabídky

![](https://arch-linux.cz/wp-content/uploads/2022/12/Snimek-obrazovky-z-2022-12-02-13-53-45-1024x327.png)

- Z **nabídky Nastavení účtu** vyberte stránku **Zabezpečení** a **kartu Dvoufázové přihlášení**

- Vyhledejte možnost **Authenticator App** a vyberte **Spravovat** : ![Manage Authenticator App]() Správa aplikace Authenticator Budete vyzváni k zadání hlavního hesla, abyste mohli pokračovat

- Na mobilním zařízení otevřete Authy a klepněte na tlačítko  **Přidat účet** .![](https://arch-linux.cz/wp-content/uploads/2022/12/Snimek-obrazovky-z-2022-12-02-13-56-31.png)

- Naskenujte QR kód umístěný ve vašem webovém trezoru pomocí Authy. Po naskenování Authy zobrazí šestimístný ověřovací kód.

- Zadejte šestimístný ověřovací kód do dialogového okna ve vašem webovém trezoru a vyberte tlačítko **Povolit** .

- Klepnutím na **tlačítko Zavřít** se vraťte na obrazovku dvoufázového přihlášení a vyberte tlačítko **Zobrazit kód obnovení** . Váš obnovovací kód lze použít v případě, že ztratíte své mobilní zařízení. **Toto je kritický krok, který zajistí, že se nikdy nedostanete do svého trezoru** , takže ho nepřeskakujte!

- Zadejte své hlavní heslo a kliknutím na **tlačítko Pokračovat** získejte kód pro obnovení. ![Example Recovery Code ]() Př

Uložte si kód pro obnovení způsobem, který vám dává největší smysl. Věřte tomu nebo ne, vytištění kódu pro obnovení a jeho uložení na bezpečném místě je jedním z nejlepších způsobů, jak zajistit, aby kód nebyl zranitelný vůči krádeži nebo nechtěnému smazání.