---
title: "IVPN: Soukromá VPN služba pro Arch Linux a Android"
date: 2025-06-07
author: "archos"
draft: false
categories: ['Návody']
tags: ['opensource', 'vpn']
---

IVPN patří mezi VPN služby, které berou soukromí vážně. Na rozdíl od většiny komerčních VPN poskytovatelů, IVPN funguje bez logování, podporuje anonymní platby a má otevřený zdrojový kód svých aplikací. Pro uživatele Arch Linuxu a mobilních zařízení nabízí solidní řešení s důrazem na bezpečnost.

## Proč IVPN?

**Žádné logování**: IVPN nemá co logovat - nesbírají IP adresy, DNS dotazy ani metadata o připojení.

**Anonymní registrace:** Účet si vygeneruješ bez osobních údajů, e-mail není potřeba. Můžete platit i kryptoměnami nebo hotovostí.

**Open source klienti**: Všechny aplikace mají otevřený zdrojový kód, takže můžete ověřit, co skutečně dělají.

**WireGuard a OpenVPN**: Podporují moderní WireGuard protokol i klasické OpenVPN.

**Multihop**: Možnost směrování přes dva VPN servery pro extra ochranu.

## Instalace na Arch Linux

### Oficiální aplikace

```bash
yay -S ivpn-ui
```

Nebo z AUR ručně:

```bash
git clone https://aur.archlinux.org/ivpn-ui.git
cd ivpn-ui
makepkg -si
```

### Spuštění a přihlášení

```bash
# Spustit daemon
sudo systemctl enable --now ivpn-daemon

# Spustit GUI
ivpn-ui
```

V aplikaci se přihlásíte pomocí Account ID, který dostanete po registraci na webu IVPN.

### Ruční konfigurace WireGuard

Pokud preferujete čistý WireGuard bez GUI:

```bash
# Instalace WireGuard
sudo pacman -S wireguard-tools

# Stáhnout konfiguraci z IVPN účtu
# Uložit jako /etc/wireguard/ivpn.conf
```

Příklad konfigurace:

```ini
[Interface]
PrivateKey = YOUR_PRIVATE_KEY
Address = 10.0.0.2/32
DNS = 172.16.0.1

[Peer]
PublicKey = SERVER_PUBLIC_KEY
Endpoint = SERVER_IP:2049
AllowedIPs = 0.0.0.0/0
```

Spuštění:

```bash
sudo wg-quick up ivpn
sudo wg-quick down ivpn
```

### Automatické spuštění

```bash
sudo systemctl enable wg-quick@ivpn
```

## Nastavení na Android

### Instalace aplikace

IVPN aplikaci najdete v Google Play Store nebo F-Droid:

```
F-Droid: https://f-droid.org/packages/net.ivpn.client/
Google Play: IVPN
```

### Konfigurace

- Otevřete aplikaci a přihlaste se pomocí Account ID
- Vyberte server (doporučuji nejbližší pro rychlost)
- Zapněte VPN přepínačem
- V nastavení můžete povolit:

Auto-connect při startu
- Kill switch (přeruší internet při výpadku VPN)
- Custom DNS servery

### WireGuard konfigurace

Alternativně můžete použít oficiální WireGuard aplikaci:

- Stáhněte si konfigurační soubor z IVPN účtu
- Importujte do WireGuard aplikace
- Aktivujte profil

## Tipy pro maximální soukromí

### DNS leak protection

```bash
# Ověření DNS úniku
dig +short myip.opendns.com @resolver1.opendns.com
```

### Firewall pravidla

```bash
# Blokovat provoz mimo VPN interface
sudo iptables -A OUTPUT ! -o tun0 -m owner --uid-owner $(id -u) -j DROP
```

### Kill switch pro systemd

Vytvořte službu, která vypne internet při odpojení VPN:

```ini
# /etc/systemd/system/vpn-killswitch.service
[Unit]
Description=VPN Kill Switch
After=network.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/local/bin/killswitch-on
ExecStop=/usr/local/bin/killswitch-off

[Install]
WantedBy=multi-user.target
```

## Rychlost a výkon

IVPN servery jsou obvykle rychlé, ale výkon závisí na:

- Vzdálenosti k serveru
- Vytížení serveru
- Vaší rychlosti internetu

Pro testování rychlosti:

```bash
speedtest-cli --secure
```

Nebo pokud nemáš speedtest-cli nainstalovaný:

```bash
# Instalace
sudo pacman -S speedtest-cli
```

## Cena a plány

IVPN má dva plány:

- **Standard**: $6/měsíc (2 současná zařízení)
- **Pro**: $10/měsíc (7 zařízení + multihop)

Platit můžete kartou, PayPal, kryptoměnami nebo hotovostí poštou.

## Alternativy

Pokud IVPN nevyhovuje, zvažte:

- **Mullvad VPN**: Podobná filozofie, €5/měsíc
- **ProtonVPN**: Free tier dostupný, Swiss privacy
- **Vlastní VPN**: WireGuard na VPS serveru

## Závěr

IVPN je solidní volba pro uživatele, kteří chtějí skutečné soukromí bez kompromisů. Open source aplikace, žádné logování a možnost anonymní registrace z něj dělají jednu z nejdůvěryhodnějších VPN služeb na trhu.

Pro Arch Linux uživatele je integrace bezproblémová díky AUR balíčku, a na Androidu funguje spolehlivě s pokročilými funkcemi jako kill switch.

Jestli bereš soukromí vážně a nechceš řešit složitou konfiguraci vlastního VPN serveru, IVPN stojí za zvážení.

## Odkazy

- 🌐 Oficiální web: [https://www.ivpn.net/en/](https://www.ivpn.net/en/)
- 💻 GitHub repozitář: [https://github.com/ivpn](https://github.com/ivpn)