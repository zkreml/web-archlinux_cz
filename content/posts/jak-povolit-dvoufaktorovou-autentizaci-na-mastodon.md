---
title: "Jak povolit dvoufaktorovou autentizaci na Mastodon"
date: 2022-11-25
author: "archos"
draft: false
categories: ['Návody']
tags: ['mastodon']
---

Dvoufaktorové ověření nabízí přidaný stupeň ochrany přístupu k vašemu Mastodon účtu. Kromě samotného hesla  k účtu je při přístupu vyžadován také ověřovací klíč, který je zasílán na Vaše mobilní zařízení. Dvoufaktorové ověření zabraňuje neoprávněným uživatelům a zařízením v přístupu k vašemu účtu.

Chcete-li povolit 2FA na Mastodon, oficiální metoda je:

**Nastavení > Nastavení účtu > Dvoufaktorové ověření > Nastavit**

![](https://arch-linux.cz/wp-content/uploads/2022/11/Snimek-obrazovky-z-2022-11-25-19-23-18-1024x481.png)

Nyní vám bude nabídnut QR kód, který můžete naskenovat pomocí aplikace [Google Authenticator](https://googleauthenticator.net/) nebo třeba pomocí u nás spravovaného správce hesel [Bitwarden](https://bitwarden.archoslinux.cz/#/login) 

![](https://arch-linux.cz/wp-content/uploads/2022/11/Snimek-obrazovky-z-2022-11-25-19-35-20-1024x481.png)

Nyní stačí v aplikaci [Bitwarden](http://bitwarden.archoslinux.cz/#/login) stisknout tlačítko Autentizační klíč (TOTP) a naskenovat QR kód, uložte. Teď opište ověřovací kód do kolonky **Kód pro dvoufázové ověření *** a  již jen **zapnout** 

Nyní máte dvoufázové ověřování zapnuté.  Ztratíte-li někdy přístup ke svému telefonu, můžete k získání přístupu k účtu použít jeden ze záložních kódů. **Uchovejte tyto kódy v bezpečí**..