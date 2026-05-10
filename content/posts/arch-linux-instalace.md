---
title: "Arch Linux Instalace"
date: 2021-12-30
author: "archos"
draft: false
categories: ['Návody', 'Arch Linux']
tags: ['instalace']
---

Velké poděkování patří uživateli [raven2cz](https://github.com/raven2cz), který připravil tento skvělý návod včetně videa. Video je již nahráno na našem [PeerTube kanále](https://peertube.arch-linux.cz/c/videa_archlinuxcz/videos?s=1).  

### Příprava zařízení pro instalaci

#### Stažení ISO a vytvoření BOOT USB disku

**[Stažení ArchLinux ISO](https://arch-linux.cz/jak-stahnout/)**, ve Win použít Rufus software (portable) na flash disk. V Linuxu použít `dd` command.

### Příprava partitions na cílovém disku

Zjistit disky a souborové systémy `fdisk -l`, pak `cfdisk /dev/`, zkontroluj kterou partition přesně použít pro umístění root adresáře, popř. domácího adresáře; např. pro nvmeXn1 bude nvmeXn1p2 nebo p3 apod. Pro EFI partition použít alespoň `+256M` parameter; nastav pro ni partition type to `EFI System (type 1)`, pro root partition `/` nastavit `Linux system`.

**DŮLEŽITÉ:** Návod používá dnes již standardní UEFI. Pokud testuje Arch dle tohoto seriálu v VirtualBox. Je nutné na záložce Systém VM **označit checkbox EFI**. Aby bylo možné používat EFI pro boot systému, jinak nepůjde instalovat bootloader.

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#vytvo%C5%99en%C3%AD-souborov%C3%BDch-syst%C3%A9m%C5%AF)Vytvoření souborových systémů

#### Formát diskových oddílů

Zvolení formátu pro diskové oddíly: `MBR` nebo `GPT`. Pro `GPT` nutno UEFI a 64bit OS. Již pro nové stanice s novým HW doporučuji `GPT` a to s dual boot pro Win10/11 + Linux.

#### Formátování diskových oddílů

Formátování EFI partition `fat`, root partition formátuji `ext4`.

```
mkfs.fat -F32 /dev/sda1
mkfs.ext4 /dev/sda2

mkswap /dev/sdxY
swapon /dev/sdxY
```

### Internetové připojení

#### Wifi

Podívejte se na [IWD-iwctl](https://wiki.archlinux.org/title/Iwd).

```
iwctl
[iwd]# device list -> opsat si označení svého wifi zařízení
[iwd]# station  get-networks -> opsat si síť, kterou potřebujete pro připojení
[iwd]# station  connect  -> připojit se ke zvolené síti a zadat heslo

druha moznost, pokud již informace máte předem zjištěné:
iwctl --passphrase  station  connect 

ping archlinux.org -> otestovaní připojení
```

### [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#ethernet)

#### Ethernet

Pouze otestovat připojení, zda internet je k dosažení.

```
ping archlinux.org
```

### Výběr Arch Mirrors

Výběr nejbližších a rychlých zrcadel balíčků archu.

Nejprve update, stažení skriptu `reflector` a záloha originální konfigurace.

```
pacman -Syy
pacman -S reflector
cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak
```

Výběr země k nalezení nejbližších bodů připojení: US, CZ, DE atd.

```
reflector -c "CZ" -f 12 -l 10 -n 12 --save /etc/pacman.d/mirrorlist
```

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#virtualbox-tty-rozli%C5%A1en%C3%AD-p%C5%99i-instalaci)

### Virtualbox tty rozlišení při instalaci

```
pacman -S fbset
fbset -g 2048 1080 2048 1080 32
```

# [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#instalace-z%C3%A1kladn%C3%ADho-syst%C3%A9mu-base)

## Instalace základního systému (Base)

Připojení (mountování) naformátované partition připravené pro root systému

```
mount /dev/sda2 /mnt
```

Preferuji instalaci aktuálního kernelu (bez speciálních úprav a zen úprav). Bez nutnosti instalace LTS kernelu (Long Term Support). Balík jádra a dalších důležitých souvisejících nástrojů je označen `linux`

Dále doporučuji nainstalovat vhodný textový editor pro úpravu konfiguračních souborů. V mém případě, co bude prezentováno je textový editor `neovim`, který spouštíte příkazem `nvim`.

```
pacstrap /mnt base base-devel linux linux-headers linux-firmware neovim nano
```

Pro úplnost ještě uvedu instalaci s možností druhého LTS kernelu. Pro základní desktop toto není nutné. V případě problémů je možné kdykoliv doinstalovat, nebo zvolit zen-kernel.

```
pacstrap /mnt base base-devel linux linux-headers linux-firmware linux-lts linux-lts-headers neovim nano
```

### Konfigurace nainstalovaného Arch systému

Generovat `fstab` soubor pro připojení diskových oddílů a služeb při spuštění systému. Přepínač `-U` je vhodný pro ukládání UUID disků, aby bylo možné jednoduše disky přehazovat a přidávat!

```
genfstab -U /mnt >> /mnt/etc/fstab
```

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#chroot)CHROOT

Vstupte do svého nového systému pomocí `chroot`.

**DÚLEŽITÉ:** Tento příkaz, kterému předchází příkaz `mount` pro root partition, je velmi užitečný pro opravu systému, reinstalace systému, opravy chyb, popřípadě volání příkazů, které vyžadují odpojený disk. USB klíčenka tak může kdykoliv sloužit pro jednoduché pořešení všech problemů. Systém se tak jednoduše stává nezničitelný.

```
arch-chroot /mnt
```

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#nastaven%C3%AD-%C4%8Dasu-a-timezone)Nastavení času a timezone

Pozor na tento bod. Je potřeba jej udělat pečlivě, dle mého postupu.

```
timedatectl list-timezones
timedatectl set-timezone Europe/Prague
ln -sf /usr/share/zoneinfo/Europe/Prague /etc/localtime
hwclock --systohc    (vygeneruje důležitý /etc/adjtime)
```

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#nastaven%C3%AD-lokalizace)Nastavení Lokalizace

Doporučuji si ponechat `US` lokalizaci. V češtině potom používat určité množiny programů a nástrojů, které jsou pro češtinu vhodné. Podobně postupují i programátoři, kteří do kódu určitě nepíší české komentáře. Myšlenkově tedy mějte oddělený jazyk pro konfigurace a jazyk pro GUI.

Editujte soubor `/etc/locale.gen` obsahující všechny dostupné lokalizace. odkomentujte potřebné lokalizace. V našem případě odkomentujte `en_US.UTF-8 UTF-8`

Nyní již můžete generovat lokalizační soubory a nakonfigurovat `locale.conf` Pokud tento krok uděláte špatně, budete mít velké problémy v mnoha programech a terminálových aplikacích, proto si pečlivě zkontrolujte následující příkazy.

```
locale-gen
echo LANG=en_US.UTF-8 > /etc/locale.conf
export LANG=en_US.UTF-8
```

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#network-konfigurace)Network konfigurace

Zadejte svůj definovaný název počítače do `/etc/hostname`. V mém případě `r7arch`. Pozor nesmí obsahovat pomlčky. Dále pak udělejte základní mapování do `/etc/hosts`.

```
echo r7arch > /etc/hostname
nvim /etc/hosts (uložte následující řádky)
127.0.0.1 localhost
::1 localhost
127.0.1.1 r7arch
```

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#nastaven%C3%AD-root-hesla)Nastavení root hesla

Nastavte své root heslo pomocí příkazu `passwd`.

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#instalace-m%C3%A9ho-fundamental-software)Instalace mého Fundamental Software

Nyní doporučuji nainstalovat naprosto fundamentální software pro přístup a základní obsluhu systému.

```
pacman -S openssh networkmanager wpa_supplicant netctl
systemctl enable NetworkManager
systemctl enable sshd

pacman -S amd-ucode (pro AMD) pacman -S intel-ucode (pro INTEL)
mkinitcpio -p linux
```

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#instalace-ovlada%C4%8D%C5%AF-a-xorg)Instalace ovladačů a Xorg

Pro desktop je nutné nainstalovat správné grafické ovladače a základní basement pro Xorg grafické rozhraní. Toto doporučiji i v případě, že budete chtít používat Wayland s plasma nebo gnome.

### [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#amd-grafick%C3%A1-karta)AMD grafická karta

```
pacman -S xorg
pacman -S mesa  (již obsažen v xorg, pouze pro informaci)
```

### [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#nvidia-grafick%C3%A1-karta)NVIDIA grafická karta

Pokud používáte LTS, nezpomeňte zvolit suffix LTS v názvu balíčků.

```
pacman -S xorg
pacman -S nvidia nvidia-utils
pacman -S nvidia-lts nvidia-utils-lts (varianta pro LTS kernel)
```

### [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#virtualbox-support)Virtualbox Support

Pokud systém testujete v virtualboxu, doporučuji nainstalovat další balíčky.

```
pacman -S virtualbox-guest-utils xf86-video-vmware
```

#### [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#nvidia-tty-nespu%C5%A1t%C4%9Bn%C3%AD-tty-termin%C3%A1lu-%C4%8Dern%C3%A1-obrazovka)NVIDIA TTY (nespuštění tty terminálu, černá obrazovka)

Nvidia kartami občas bývá problém, dlouhé diskuze zde vést nebudu. Doporučuji přidat nvidia do KMS. Tento krok můžete udělat/neudělat kdykoliv bude potřeba, pokud ale máte černou obrazovku po restartu systému, budete toto muset udělat hned.

```
sudo vim /etc/mkinitcpio.conf
(editovat následující dvě řádky v souboru)
MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)
FILES="/etc/modprobe.d/nvidia.conf

sudo mkinitcpio -P
nvim /etc/modprobe.d/nvidia.conf
(přidat tuto řádku do souboru a uložit)
options nvidia_drm modeset=1
```

Ještě pro jistotu doporučuji přidat `*nvidia-drm.modeset=1` do příkazů při spuštění kernelu v `grub.cfg` (pokud používáte grub). Viz dokument [https://wiki.archlinux.org/index.php/kernel\_parameters](https://wiki.archlinux.org/index.php/kernel_parameters](https://wiki.archlinux.org/index.php/kernel/_parameters](https://wiki.archlinux.org/index.php/kernel_parameters)

Později po restartu systému (teď ještě nerestartovat!) ověřit si správné instalovanou nvidia kartu pomocí příkazu

```
lspci -vnn | grep VGA
```

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#p%C5%99id%C3%A1n%C3%AD-u%C5%BEivatele-linuxu)Přidání uživatele Linuxu

Nyní již můžeme přidat naše uživatele linuxu. Nutno v příkazech zaměnit `` za vaše jméno. Já v ukázkách používám jméno uživatele `box`.

Velmi užitečnou výhodou v archu je použití již připravených skupin: `storage` a `power`. Umožňují jednoduše používat mountování disků a vypínání/restart systému přímo uživatelem, bez nutnosti dalších berliček.

```
useradd -m -g users -G wheel,storage,power -s /bin/bash 
passwd 
pacman -S sudo
EDITOR=nvim visudo,  (odkomentovat řádku) %wheel ALL=(ALL) ALL
```

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#instalace-bootloader-grub2)Instalace Bootloader Grub2

Instalace bootloaderu pro možnost dual boot s windows, popř. přepínání s dalšími operačními systémy. Rovněž konfigurace dostupných kernelů pro zavedení a spuštění. Zde je celá řada možností. Uvádím zde jedno z nejstarších řešení.

```
pacman -S grub efibootmgr dosfstools os-prober mtools
```

Vytvoření adresáře kde bude mountována EFI partition:

```
mkdir /boot/efi
```

Nyní připojíme EFI partition, kterou jsme dříve vytvořili v prvním kroku instalace.

```
mount /dev/sda1 /boot/efi
```

Instalace grub2 například takto pro UEFI:

```
grub-install --target=x86_64-efi --bootloader-id=ARCH --efi-directory=/boot/efi --recheck
```

V tomto případě potom budeme mít v biosu v nabídce jméno EFI části `ARCH` (bootloader-id).

Nakonec se musí zavolat natažení konfigurace do `grub.cfg`

```
grub-mkconfig -o /boot/grub/grub.cfg
```

Základní systém je hotov.

## [](https://github.com/raven2cz/tux/tree/main/210906-arch-instalace#restart-z%C3%A1kladn%C3%ADho-syst%C3%A9mu-a-jeho-test)Restart základního systému a jeho test

Nejprve regulerně opustě chroot prostředí pomocí `exit` příkazu nebo klávesovou zkratkou `ctrl+d`. Volitelně můžete odpojit mountované disky `umount -R /mnt`.

Nakonec zavolejte:

```
reboot
```

Po restartu systému se spustí grub2 a po správném zavedení systému se objeví tty terminál se zadáním uživatelského jména a zvoleného hesla.

Po úspěšném přihlášení jste ve svém novém Arch systému! Vítejte doma ![](https://github.githubassets.com/images/icons/emoji/unicode/1f427.png)

https://www.youtube.com/watch?v=gpIFaCIB9Cg&t=1170s

# Důležité odkazy

- [Youtube Channel TUX: Svět Linuxu](https://www.youtube.com/user/tondafischer/featured)

- [archlinux.org](https://archlinux.org/)

- [wiki.achlinux.org](https://wiki.archlinux.org/)

- [fishlive.org/blog](https://fishlive.org/en/blog-tech-art/arch)

- [github/raven2cz/tux](https://github.com/raven2cz/tux)

- [github/raven2cz/dotfiles](https://github.com/raven2cz/dotfiles)