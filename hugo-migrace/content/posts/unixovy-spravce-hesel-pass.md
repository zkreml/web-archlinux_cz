---
title: "Unixový správce hesel Pass"
date: 2023-02-10
author: "raven2cz"
draft: false
categories: ['Návody']
tags: ['pass']
---

### Co je správce hesel PASS

Pass je správce hesel příkazového řádku vytvořený s ohledem na filozofii Unixu. Umožňuje vám pracovat s vašimi hesly pomocí běžných unixových příkazů. Přihlašovací údaje jsou uloženy v souborech zašifrovaných GPG.

### PASS je komplikovaný! Jen pro geeky!

Toto je typická odpověď mnoha uživatelů, kteří pláčou na fórech. Ale není to pravda. Jakákoli technologie potřebuje znát některé základy používání. Pokud chcete řídit auto nebo hrát World of Warcraft, musíte se nejprve naučit základy. Abyste byli PRO, potřebujete víc. Pro základní a standardní uživatelské použití **je pass jednoduchý a efektivní nástroj** .

## [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#gnupg-basics)

## Základy GnuPG

Prvním základním know-how pro *nix je použití pgp klíčů a možnost šifrovat/dešifrovat a podepisovat vaši práci a soubory.

[https://wiki.archlinux.org/title/GnuPG](https://wiki.archlinux.org/title/GnuPG)

```
sudo pacman -S gnupg
nvim ~/.gnupg/gpg-agent.conf 
  pinentry-program /usr/bin/pinentry-curses
  pinentry-program /usr/bin/pinentry-gnome3
  max-cache-ttl 60480000
  default-cache-ttl 60480000

# create new key-pair, follow questions, select master password reasonably
gpg --full-gen-key

# export/import your keys
gpg --export --armor --output public.key user-id
gpg --import public.key
gpg --export-secret-keys --armor --output privkey.asc user-id
gpg --import privkey.asc

# make your key ultimate and default
gpg --edit-key user-id/key
type in cli: trust, choice 5, save, quit

# search your keys
gpg --search-keys user-id

# optional upload your gpg public key to key servers
https://keys.openpgp.org
https://keyserver.ubuntu.com/

# encrypt/decrypt files example - asymmetric
gpg --recipient user-id --encrypt doc
gpg --output doc --decrypt doc.gpg
```

## Pass základy

### [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#directory-hierarchy)

### Hierarchie adresářů

Adresářová struktura závisí na vás. Preferuji používání passu **nejen** pro správu přihlašivacích hesel!

Moje hierarchie je následující

- credit-cards

- finance

- local

- login

- ssid

- token

Podsložky v `login`syntaxe složky

- url/uživatelské jméno (pokud je více uživatelů nebo účtů)

- url (pouze jednoduchá adresa URL bez názvu účtu)

Podsložky v `login`příklady složek

```
├── logitech.com
   ├── mail.plzen-edu.cz
   ├── malirskeplatna.cz
   ├── mall.cz
   ├── mastodon.arch-linux.cz
   ├── jira.cloud.cz
   │   ├── andrew
   │   ├── antfis
   │   └── petr
```

### [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#syntax-inside-encrypted-gpg-file)

### Syntaxe uvnitř zašifrovaného souboru gpg

První řádek patří heslu podle `pass`   syntax. Všechny další řádky jsou volitelné dle vašeho přání. U kreditních karet můžete pro podrobnosti potřebovat mnohem více řádků. **Můžete si uložit vše, co potřebujete. Je to pouze textový soubor.**

Je tu jeden důležitý bod!

Pokud chcete použít `passff` nebo jiná rozšíření, musíte použít `login:` řádek s názvem vašeho účtu, do kterého bude automaticky vložen `login field`  v přihlašovacím formuláři webové stránky.

```
password
login: account
```

### [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#fundamental-commands)

### Základní příkazy

```
# initialize the password store
pass init gpg-id_or_email

# insert new password for archlinux.org with defined username
# this insert is optional, I'm using mainly 'generate' and 'edit' command
pass insert login/archilinux.org
pass insert login/archlinux.org/username

# generate password with N symbols, example with length 20
pass generate archlinux.org/wiki/username -n 20

# edit file to fill additional details - 'login:' row, etc.
# edit command will use your $EDITOR, nvim, emacs etc.
pass edit archlinux.org/wiki/username

# publish changes directly to git private repo, no commit needed!
# needs linkage with git first, see next chapters...
pass git push

# direct copy to clipboard
pass -c login/archlinux.org
# or integration with rofi, dmenu
rofi-pass
passmenu

# pass fulltext search
pass search archlinux
```

## [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#git-private-repo-integration)

## Integrace soukromého Git repozitáře

### [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#server-side)

### Nastavení na  straně serveru

Nejprve vytvořte `git bare private-repo`  na vašem serveru, soukromém domácím cloudu nebo soukromém cloudovém úložišti git (tato poslední volba není z mé strany preferována). Je to standardní git repozitář, který bude ukládat vaše zakódované soubory gpg a adresářovou strukturu.

Pokud nevíte nic o git nebo git serverech. Postupujte podle předchozího článku `git-bare-repo` nebo si jen přečtěte články o GitHubu a základní tutoriály git.

### [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#client-side)

### Nastavení na straně klienta

```
# create local password store
pass init 
# Enable management of local changes through Git
pass git init
# Add the the remote git repository as 'origin'
pass git remote add origin user@server:~/.password-store
# Push your local pass history
pass git push -u --all

# just work with pass and git
pass git pull
pass generate ...
pass edit ...
pass git push
# DONE.

# all git operations work normally just with prefix 'pass'
```

### [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#pass-new-station-installation-steps)

### Projděte kroky instalace nové stanice

Pokud máte nový počítač a potřebujete `pass` a vaše úložiště na nové stanici. Můžete vytvořit nějaký malý skript, nebo stačí napsat těchto pár příkazů.

```
# install software
sudo pacman -S gnupg pass rofi-pass git

# import public and private keys
gpg --import gpg-public.key
gpg --import privkey.asc

# ultimate access for your gpg key for new station
gpg --edit-key user-idOrkey-id
type in cli: trust, choice 5, save, quit 

# clone your git repostiory to .password-store
git clone gitlab@server:repo/pass-store.git ~/.password-store

# configure your pass git
pass git config --global user.email "email" 
pass git config --global user.name "name"
pass git config --global user.signingkey 

# gpg and pinetry check or add
nvim ~/.gnupg/gpg-agent.conf 
	pinentry-program /usr/bin/pinentry-gnome3
```

## [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#rofidmenu-integration)

## Integrace Rofi/dmenu

[![pass-zx2c4-rofi](https://github.com/raven2cz/geek-room/raw/main/attachments/pass-zx2c4-rofi.png)](https://github.com/raven2cz/geek-room/blob/main/attachments/pass-zx2c4-rofi.png)

Rofi a dmenu má rychlé a výkonné použití s ​​passem

```
sudo pacman -S rofi-pass 
rofi-pass
passmenu
```

```
# example integration with awesomewm
awful.key({modkey, altkey},"p",function() awful.spawn.with_shell("rofi-pass -t") end,
          {description="types password from pass", group="launcher"}),
awful.key({modkey, ctrlkey},"p", function() awful.spawn.with_shell("rofi-pass") end,
          {description="copy password from pass", group="launcher"}),
```

## [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#passff---firefox-integration)

## Passff - integrace do Firefoxu

![](https://arch-linux.cz/wp-content/uploads/2023/02/pass-zx2c4-passff.png)

Nainstalujte `passff`rozšíření do vašeho Firefoxu z Firefox Extension Storage.

Vytvořit `host`spojení, komunikační protokol mezi systémem a rozšířením passff. To se nazývá `passff-host`; tato aplikace má implementaci pro každou distribuci. Pro Arch můžete použít balíček AUR.

```
% git clone https://aur.archlinux.org/passff-host.git/
% cd passff-host
% makepkg -si
```

## [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#browserpass---brave-chromium-firefox-integration)

## browserpass – integrace Brave, Chromium, Firefox

![](https://arch-linux.cz/wp-content/uploads/2023/02/pass-zx2c4-browserpass.png)

Nainstalujte `browserpass` z úložiště rozšíření prohlížeče. O projektu [zde](https://github.com/browserpass/browserpass-extension) .

Integrace s vaším systémem, podobně jako `passff-host`

```
paru -S browserpass
Nainstalujte browserpass úložiště rozšíření prohlížeče.

Integrace s vaším systémem, podobně jako passff-host

paru -S browserpass
```

## Password Store, OpenKeychain – integrace se systémem Android

Stačí nainstalovat obě aplikace pro Android. První `PasswordStore` aplikace musí být v telefonu prohozena s výchozím správcem hesel nebo pouze v nastavení prohlížeče. Druhý `OpenKeychain` aplikace je úložiště pro vaše soukromé a veřejné klíče gpg a poskytuje API pro `PasswordStore`.

`PasswordStore`  má plnou podporu pro soukromé repozitáře git, git pull a push funguje z nabídky.

S tímto řešením nemám žádné chyby a toto úložiště a správce hesel používám několik let.

## [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#windows-integration---wsl2)

## Integrace Windows - WSL2

Integrace MS Windows a WSL2 je pokročilé téma. Napsal jsem   [o tom jiný článek](https://fishlive.org/en/blog-tech-art/pass-zx2c4-and-passff-for-wsl2-windows) .

## [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#next-apps-and-possibilities)

## Další Aplikace a možnosti

Sledujte [domovskou stránku pass](https://www.passwordstore.org/) dole!

- Kompatibilní klienti

- Migrace z jiných klientů

Například **Gopass** .

![](https://arch-linux.cz/wp-content/uploads/2023/02/pass-zx2c4-gopass.png)

[https://github.com/gopasspw/gopass](https://github.com/gopasspw/gopass)

## [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#pass---credit--license)

## Pass - Credit & License

pass was written by Jason A. Donenfeld of [zx2c4.com](https://zx2c4.com) and is licensed under the [GPLv2+](http://www.gnu.org/licenses/gpl-2.0.html).

https://www.youtube.com/watch?v=MrvWrBaYTyI

#### Důležité odkazy:

- [https://www.passwordstore.org/](https://www.passwordstore.org/)

- [https://wiki.archlinux.org/title/GnuPG](https://wiki.archlinux.org/title/GnuPG)

- [https://wiki.archlinux.org/title/Pass](https://wiki.archlinux.org/title/Pass)

- [https://github.com/passff/passff](https://github.com/passff/passff)

- [https://github.com/passff/passff-host](https://github.com/passff/passff-host)

- [https://github.com/browserpass/browserpass-extension](https://github.com/browserpass/browserpass-extension)

- [Password Store](https://play.google.com/store/apps/details?id=dev.msfjarvis.aps&hl=cs&gl=US) + [OpenKeychain](https://play.google.com/store/apps/details?id=org.sufficientlysecure.keychain&hl=cs&gl=US) (Android Google Play)

- [pass project source code](https://git.zx2c4.com/password-store) a [mirror](https://github.com/zx2c4/password-store)

- [https://fishlive.org/en/blog-tech-art/pass-zx2c4-and-passff-for-wsl2-windows](https://fishlive.org/en/blog-tech-art/pass-zx2c4-and-passff-for-wsl2-windows)

- [GitHub autora](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4)

## [](https://github.com/raven2cz/geek-room/tree/main/pass-zx2c4#depends-on)

#### Závisí na:

- bash [http://www.gnu.org/software/bash/](http://www.gnu.org/software/bash/)

- GnuPG2 [http://www.gnupg.org/](http://www.gnupg.org/)

- git [http://www.git-scm.com/](http://www.git-scm.com/)

- xclip (for X11 environments) [http://sourceforge.net/projects/xclip/](http://sourceforge.net/projects/xclip/)

- wl-clipboard (for wlroots Wayland-based environments) [https://github.com/bugaevc/wl-clipboard](https://github.com/bugaevc/wl-clipboard)

- tree >= 1.7.0 [http://mama.indstate.edu/users/ice/tree/](http://mama.indstate.edu/users/ice/tree/)

- GNU getopt [http://www.kernel.org/pub/linux/utils/util-linux/](http://www.kernel.org/pub/linux/utils/util-linux/) [http://software.frodo.looijaard.name/getopt/](http://software.frodo.looijaard.name/getopt/)

- qrencode [https://fukuchi.org/works/qrencode/](https://fukuchi.org/works/qrencode/)