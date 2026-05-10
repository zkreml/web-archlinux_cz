---
title: "Šifrovaná instalace Arch Linux pomocí Calam-Arch-Installer"
date: 2022-03-03
author: "archos"
draft: false
categories: ['Návody']
tags: ['btrfs', 'calamares']
---

## Úvod

Pro začátečníka může být složité až skoro nemožné Arch Linux nainstalovat a nakonfigurovat podle svých
potřeb. Někoho může i instalace v příkazovém řádku odradit. V dnešním návodu si ukážeme, jak
nainstalovat Arch Linux pomocí instalátoru Calam-Arch-installer. Tento návod předpokládá,že Arch
Linux bude jediným OS v zařízení.

## Co získáme instalací

• Plně LUKS šifrovaný oddíl obsahující souborový systém BTRFS s / boot, / root a / home
• / a /home jako samostatné dílčí svazky, které umožňují snadnou a úložnou úsporu místa
snímků kořenového systému
• automatické vytváření snímků (při upgradu systému a každodenním a bootování)
• schopnost zavést do funkčního snímku z nabídky grub (automatické vytváření spouštěcích
položek) a poté nastavit tento nebo jiný snímek jako nový výchozí systém (z grafického
uživatelského rozhraní)

## Stažení a příprava instalačního USB

Nejprve si stáhneme ISO [Calam-Arch-Installer](https://sourceforge.net/projects/blue-arch-installer/)  Obraz zapíšeme na USB disk třeba pomocí nástroje
Etcher.Restartujeme počítač a při zavádění systému v BIOSu nastavíme zavádění systému pomocí
USB.
Pří zavádění z USB se vám ukáže úvodní obrazovka instalátoru

![](https://arch-linux.cz/wp-content/uploads/2022/02/instalace1.png)

## Příprava instalace

Nejdříve je třeba udělat pár maličkostí před instalací našeho nového systému.
Změňte výchozí nastavení btrfs calamar pro fstab.Následující krok vynutí, aby calamar přiřadil a
používal kompresi na všech instalačních zařízeních btrfs; bez ohledu na to, zda jsou ssd nebo
hdd. Použijeme kompresi zstd.
Otevřete Terminal,Firefox s naším návodem a zadejte (nebo označte a zkopírujte níže uvedené
příkazy pomocí ctrl-c a vložte do terminálu pomocí shift-ctrl-v | vždy můžete kopírovat a vložit
všechny řádky zobrazené v jednom bloku najednou)

```
sudo sed -i 's/compress=lzo/compress=zstd/'
/usr/share/calamares/modules/fstab.conf
sudo sed -i 's/autodefrag/autodefrag,compress=zstd/'
/usr/share/calamares/modules/fstab.conf
```

 Terminál necháme otevřený a můžeme přistoupit k samotné instalaci.

## Instalace systému

Instalátor [Calam-Arch-Installer](https://sourceforge.net/projects/blue-arch-installer/) je založený na instalačním frameworku [Calamares](https://calamares.io/), který používají i
jiné linuxové distribuce EndeavourOS, Manjaro, Arcolinux a mnoho dalších.
Instalátor nám položí několik otázek. Nejdříve nastavíme jazyk systému.

![](https://arch-linux.cz/wp-content/uploads/2022/02/instalace_vyber_jazyka3.png)*výběr jazyka*

Nastavíme časové pásmo.

![](https://arch-linux.cz/wp-content/uploads/2022/02/casove_pasmo4.png)*výběr časového pásma*

V dalším kroku vybereme požadované rozložení klvesnice

![](https://arch-linux.cz/wp-content/uploads/2022/02/vyber_klavesnice5.png)*rozložení klávesnice*

Nyní přejdeme k rozdělení disku.Nejdříve vytvoříme novou tabulku oddílů a jako typ oddílu
zvolíme [GPT](https://cs.wikipedia.org/wiki/GUID_Partition_Table) zadáním ok,vytvoříme tabulku.

![](https://arch-linux.cz/wp-content/uploads/2022/02/nova-tabulka-oddilu6.png)*Vytvoření tabulky GPT*

Dále zvolíme ruční rozdělení disku a vytvoříme oddíl 512MB Fat 32 s přípojným bodem /boot a s
příznakem boot. Tímto vytvoříme systémový oddíl EFI.

![](https://arch-linux.cz/wp-content/uploads/2022/02/rucni-rozdeleni-disku.png)*ruční rozdělení disku*

![](https://arch-linux.cz/wp-content/uploads/2022/02/vytvoreni_efi7.png)

Na zbytku volného místa vytvoříme souborový systém BTRFS, zaškrtneme šifrování a zvolíme
heslo.
Přípojný bod pro tento oddíl bude /

![](https://arch-linux.cz/wp-content/uploads/2022/02/zbytek_btrfs8.png)*Oddíl BTRFS*

V dalším kroku vybereme jaké chceme použít grafické prostředí, ovladače grafické karty a nebo
veškeré balíčky pro správu tisku.

![](https://arch-linux.cz/wp-content/uploads/2022/02/vyber-prostredi9.png)

V dalším kroku vytvoříme uživatele, heslo pro přihlášení do systému.

![](https://arch-linux.cz/wp-content/uploads/2022/02/vytvoreni_uzivatele10.png)*vytvoření uživatele*

Klikneme na další a systém se nám nainstaluje. Po dokončení instalace systém
**NERESTARTOVAT**,
ale zadáme ještě několik příkazů. Prvním příkazem vytvoříme odkládací prostor. 8G nahradíme 
požadovanou velikostí.

```
swapsize=8G
```

Po vytvoření oddílu spustíme další příkazy.Stáčí je jen všechny zkopírovat (ctrl+c) a následně vložit
do terminálu (ctrl+shift+v)

```
sudo mkdir /mnt/btrfs
btrfsonluks=`sudo blkid -o device | grep luks`
sudo mount -o subvolid=5 $btrfsonluks /mnt/btrfs
sudo sed -i 's/compress=zstd 0 1/compress=zstd 0 0/' /mnt/btrfs/@/etc/fstab
sudo sed -i 's/compress=zstd 0 2/compress=zstd 0 0/' /mnt/btrfs/@/etc/fstab
sudo btrfs subvolume create /mnt/btrfs/@var-cache-pacman-pkg
fstabstr=`grep "/home" /mnt/btrfs/@/etc/fstab`
fstabstr=${fstabstr//\/home/\/var\/cache\/pacman\/pkg}
fstabstr=${fstabstr//@home/@var-cache-pacman-pkg}
sudo sh -c "echo $fstabstr >> /mnt/btrfs/@/etc/fstab"
sudo btrfs subvolume create /mnt/btrfs/@swap
sudo mkdir /mnt/btrfs/@/swap
sudo sh -c "printf '\n$btrfsonluks /swap
btrfs
subvol=@swap,defaults,compress=no 0 0\n' >> /mnt/btrfs/@/etc/fstab"
sudo truncate -s 0 /mnt/btrfs/@swap/swapfile
sudo chattr +C /mnt/btrfs/@swap/swapfile
sudo btrfs property set /mnt/btrfs/@swap/swapfile compression none
sudo fallocate -l $swapsize /mnt/btrfs/@swap/swapfile
sudo chmod 600 /mnt/btrfs/@swap/swapfile
sudo mkswap /mnt/btrfs/@swap/swapfile
sudo swapon /mnt/btrfs/@swap/swapfile
sudo sh -c "echo '/swap/swapfile none swap defaults 0 0' >>
/mnt/btrfs/@/etc/fstab"
wget https://raw.githubusercontent.com/osandov/osandov-linux/master/scripts/
btrfs_map_physical.c
gcc -O2 -o btrfs_map_physical btrfs_map_physical.c
offset=`sudo ./btrfs_map_physical /mnt/btrfs/@swap/swapfile`
offset_arr=(`echo ${offset}`)
offset_pagesize=(`getconf PAGESIZE`)
offset=$(( offset_arr[25] / offset_pagesize ))
sudo sed -i "s/loglevel=3/loglevel=3 resume_offset=$offset/"
/mnt/btrfs/@/etc/default/grub
sudo sed -i "s#loglevel=3#resume=$btrfsonluks loglevel=3#"
/mnt/btrfs/@/etc/default/grub
sudo sed -i 's/keymap encrypt filesystems/keymap encrypt filesystems resume/'
/mnt/btrfs/@/etc/mkinitcpio.conf
sudo mkdir /mnt/chroot
sudo mount -o compress=zstd,subvol=@ $btrfsonluks /mnt/chroot
efidevice=`sudo blkid -o device -l -t TYPE=vfat`
sudo mount $efidevice /mnt/chroot/boot/efi
sudo arch-chroot /mnt/chroot
sudo pacman --noconfirm -S cronie
sudo systemctl enable cronie.service
sudo grub-mkconfig -o /boot/grub/grub.cfg
sudo mkinitcpio -p linux
```

Nyní můžeme restartovat počítač.

## Nový systém

Po restartu a přihlášení do nového systému, musíme nejdřív nainstalovat pomocníka YAY pro AUR
repozitář. V AUR repozitáři se nachází zálohovací program Timeshift.

```
pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

Nyní nainstalujeme program Timeshift a potřebné závislosti.

```
sudo pacman --noconfirm -Syy &&
yay --noconfirm -S timeshift timeshift-autosnap grub-btrfs
```

Poté spustíme následující příkazy

```
sudo cp /etc/timeshift/default.json /etc/timeshift/timeshift.json &&
fs_uuid=`sudo blkid -o device | grep luks` &&
fs_uuid=`sudo blkid -o value -s UUID $fs_uuid` &&
sudo sed -i "s/backup_device_uuid\" : \"/backup_device_uuid\" : \"$fs_uuid/"
/etc/timeshift/timeshift.json &&
fs_uuid=`sudo blkid -o device -l -t TYPE=crypto_LUKS` &&
fs_uuid=`sudo blkid -o value -s UUID $fs_uuid` &&
sudo sed -i "s/parent_device_uuid\" : \"/parent_device_uuid\" : \"$fs_uuid/"
/etc/timeshift/timeshift.json &&
sudo sed -i 's/run" : "true/run" : "false/' /etc/timeshift/timeshift.json &&
sudo sed -i 's/btrfs_mode" : "false/btrfs_mode" : "true/'
/etc/timeshift/timeshift.json &&
sudo sed -i 's/ "include_btrfs_home" : "false",/
"include_btrfs_home_for_backup" : "false",\n "include_btrfs_home_for_restore" :
"false",/' /etc/timeshift/timeshift.json &&
sudo sed -i 's/schedule_daily" : "false/schedule_daily" : "true/'
/etc/timeshift/timeshift.json &&
sudo sed -i 's/schedule_boot" : "false/schedule_boot" : "true/'
/etc/timeshift/timeshift.json &&
sudo sed -i 's/count_boot" : "5/count_boot" : "3/' /etc/timeshift/timeshift.json
sudo timeshift --create --comments "1st"
```

## Omezení maximálního počtu snímků

```
max_snapshots=6
```

A jako poslední spustgíme příkazy.

```
sudo sh -c '
cat > /etc/systemd/system/limit-timeshift-snapshots-update-grub.service $max_snapshots'\` \&\& /usr/bin/grub-mkconfig -o /boot/grub/grub.cfg\"#"
/etc/systemd/system/limit-timeshift-snapshots-update-grub.service &&
sudo systemctl enable limit-timeshift-snapshots-update-grub.service &&
sudo systemctl start limit-timeshift-snapshots-update-grub.service
```

**A je to**
nyní máte plně šifrovaný systém Arch Linux, s aumaticky vytvořenými snímky. Stačí jen při
botování vybrat k jakému snímku se potřebujete vrátit.

![](https://arch-linux.cz/wp-content/uploads/2022/02/grub11.png)*nový systém*