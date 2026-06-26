# Shelly-ALPM – Moderní správce balíčků pro Arch Linux

*Alternativa k pacmanu, která mluví lidsky*

---

## 1. Co je Shelly?

Shelly je grafický i příkazový správce balíčků pro Arch Linux. Na rozdíl od většiny alternativ (octopi, pamac) **není wrapper nad pacmanem** – komunikuje přímo s knihovnou `libalpm`, tedy se stejným jádrem, které používá samotný pacman.

Projekt vyvíjí Zoey Bauer pod hlavičkou Seafoam Labs. Je psaný v C# (.NET 10), GUI běží na GTK 4 s nativní podporou Waylandu. Licence je GPL-3.0.

---

## 2. Proč by tě to mělo zajímat?

Pacman je skvělý nástroj, ale jeho syntaxe není zrovna intuitivní. Porovnej:

```bash
# pacman
sudo pacman -Syu firefox
sudo pacman -Rns firefox
pacman -Ss firefox

# shelly
shelly install firefox
shelly remove firefox
shelly search firefox
```

Shelly nabízí jednotnou, čitelnou syntaxi a k tomu moderní GUI, kde na jednom místě zvládneš oficiální repozitáře, AUR i Flatpak.

---

## 3. Hlavní vlastnosti

- **CLI + GUI** – `shelly` pro terminál, `shelly-ui` pro grafické rozhraní
- **Přímá integrace s libalpm** – žádný wrapper, žádná mezivrstva
- **AUR podpora** – vyhledávání, instalace i aktualizace AUR balíčků
- **Flatpak podpora** – správa Flatpak aplikací včetně instalace z FlatpakRef souborů
- **Notifikace** – `shelly-notifications` běží v tray a upozorní na dostupné aktualizace
- **Nativní Wayland** – GUI postavené na GTK 4
- **Themování** – Shelly používá čisté GTK bez libadwaita, takže respektuje tvoje systémové téma

---

## 4. Instalace

### CachyOS (v oficiálních repozitářích)

```bash
sudo pacman -Syu shelly
```

### AUR (pro čistý Arch a další deriváty)

```bash
yay -S shelly
```

nebo

```bash
paru -S shelly
```

### Ruční build z GitHubu

```bash
git clone https://github.com/Seafoam-Labs/Shelly-ALPM.git
cd Shelly-ALPM
makepkg -si
```

Po instalaci máš k dispozici tři binárky:

```bash
shelly          # CLI
shelly-ui       # GUI
shelly-notifications  # tray notifikace
```

---

## 5. Základní použití – CLI

### Synchronizace databáze

```bash
shelly sync
shelly sync --force    # vynutí refresh i když je DB aktuální
```

### Aktualizace systému

```bash
shelly upgrade
shelly upgrade --no-confirm   # bez potvrzení
```

### Instalace a odebírání balíčků

```bash
shelly install firefox vim
shelly remove firefox
```

### Hledání balíčků

```bash
shelly list-installed     # nainstalované balíčky
shelly list-available     # dostupné balíčky
shelly list-updates       # balíčky s dostupnou aktualizací
```

### Instalace lokálního balíčku

```bash
shelly install-local /cesta/k/balicku.pkg.tar.zst
```

---

## 6. AUR příkazy

```bash
shelly aur search neovim       # hledání v AUR
shelly aur install neovim-git  # instalace z AUR
shelly aur list                # nainstalované AUR balíčky
shelly aur list-updates        # AUR balíčky s aktualizací
shelly aur upgrade             # aktualizace všech AUR balíčků
shelly aur remove neovim-git   # odebrání AUR balíčku
```

---

## 7. Flatpak příkazy

```bash
shelly flatpak search signal         # hledání na Flathubu
shelly flatpak install org.signal.Signal  # instalace
shelly flatpak list                   # nainstalované Flatpak aplikace
shelly flatpak upgrade               # aktualizace všech
shelly flatpak uninstall org.signal.Signal  # odebrání
shelly flatpak run org.signal.Signal  # spuštění
```

---

## 8. Konfigurace

Při prvním spuštění se vytvoří konfigurační soubor:

```
~/.config/shelly/config.json
```

Příklad obsahu:

```json
{
  "FileSizeDisplay": "Megabytes",
  "DefaultExecution": "UpgradeAll"
}
```

- **FileSizeDisplay** – formát velikosti souborů: `Bytes`, `Megabytes`, `Gigabytes`
- **DefaultExecution** – co se stane při spuštění `shelly` bez parametrů: `UpgradeAll`, `UpgradeStandard`, `UpgradeFlatpak`, `UpgradeAur`, `Sync`, `SyncForce`, `ListInstalled`

---

## 9. Srovnání s pacmanem

| Akce | pacman | shelly |
|---|---|---|
| Aktualizace systému | `sudo pacman -Syu` | `shelly upgrade` |
| Instalace balíčku | `sudo pacman -Syu balíček` | `shelly install balíček` |
| Odebrání balíčku | `sudo pacman -Rns balíček` | `shelly remove balíček` |
| Hledání balíčku | `pacman -Ss balíček` | `shelly list-available` |
| Nainstalované balíčky | `pacman -Q` | `shelly list-installed` |
| Dostupné aktualizace | `checkupdates` | `shelly list-updates` |
| Synchronizace DB | `sudo pacman -Sy` | `shelly sync` |
| AUR instalace | `yay -S balíček` | `shelly aur install balíček` |

---

## 10. Co je v plánu?

Podle roadmapy projektu se chystá:

- Správa repozitářů přímo z GUI
- Podpora AppImage (ve stylu GearLever)
- Vylepšená Flatpak integrace
- Import seznamu balíčků – obnovení systému do uloženého stavu
- Ikony pro standardní balíčky při vyhledávání
- Spouštění aktualizací přímo z notifikací

---

## 11. Pro koho je Shelly?

Shelly se hodí hlavně pro:

- **Začátečníky na Archu** – GUI + čitelné příkazy snižují bariéru vstupu
- **Uživatele CachyOS** – Shelly je součástí oficiálních repozitářů
- **Kohokoliv, kdo chce AUR + Flatpak + pacman na jednom místě**

Pro zkušené uživatele, kteří mají pacman v krvi a nepotřebují GUI, je Shelly spíš doplněk než náhrada. Ale ta CLI syntaxe je fakt příjemnější.

---

## Cheat sheet

```
╔══════════════════╦════════════════════════════════════════════════╗
║ KATEGORIE        ║ PŘÍKAZ                                        ║
╠══════════════════╬════════════════════════════════════════════════╣
║ SYSTÉM           ║                                                ║
║                  ║ shelly sync           → synchronizace DB       ║
║                  ║ shelly upgrade        → aktualizace systému    ║
║                  ║ shelly list-updates   → dostupné aktualizace   ║
╠══════════════════╬════════════════════════════════════════════════╣
║ BALÍČKY          ║                                                ║
║                  ║ shelly install pkg    → instalace              ║
║                  ║ shelly remove pkg     → odebrání               ║
║                  ║ shelly list-installed → nainstalované           ║
║                  ║ shelly install-local  → lokální balíček        ║
╠══════════════════╬════════════════════════════════════════════════╣
║ AUR              ║                                                ║
║                  ║ shelly aur search     → hledání v AUR          ║
║                  ║ shelly aur install    → instalace z AUR        ║
║                  ║ shelly aur upgrade    → aktualizace AUR        ║
║                  ║ shelly aur list       → nainstalované AUR      ║
╠══════════════════╬════════════════════════════════════════════════╣
║ FLATPAK          ║                                                ║
║                  ║ shelly flatpak search → hledání na Flathubu    ║
║                  ║ shelly flatpak install→ instalace              ║
║                  ║ shelly flatpak upgrade→ aktualizace všech      ║
║                  ║ shelly flatpak list   → nainstalované          ║
╠══════════════════╬════════════════════════════════════════════════╣
║ GUI              ║                                                ║
║                  ║ shelly-ui             → grafické rozhraní      ║
║                  ║ shelly-notifications  → tray notifikace        ║
╚══════════════════╩════════════════════════════════════════════════╝
```

---

**Odkazy:**

- GitHub: [github.com/Seafoam-Labs/Shelly-ALPM](https://github.com/Seafoam-Labs/Shelly-ALPM)
- Web: [shellyalpm.com](https://shellyalpm.com)
- Licence: GPL-3.0
