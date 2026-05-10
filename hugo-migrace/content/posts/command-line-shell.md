---
title: "Command-Line Shell"
date: 2022-04-01
author: "archos"
draft: false
categories: ['Návody']
tags: ['shell']
series: ['Arch Linux instalace']
---

V dalším díle seriálu [Tondy Fischera](https://github.com/raven2cz) se podíváme na prostředí příkazového řádku. Představíme si postupně 3 nejrozšířenější shelly v GNU/Linux (sh nepočítám). Shells si postupně nakonfigurujeme a přizpůsobíme opět pro nejlepší efektivitu svojí práce. Terminálové aplikace se tak dostanou na zcela jinou úroveň, se kterou se často nemohou měřit ani normální aplikace s tlačítky. Batch processing je nenahraditelnou součástí pokročilého používání počítačů, historie příkazů a fuzzy processing je něco, co se jiným operačním systémům ani nesnilo.

Popis shellů je uveden na arch wiki [Command-Line Shell](https://wiki.archlinux.org/title/Command-line_shell).

Základní shelly, které si ukážeme:

- `Bash` - nejzákladnější shell v GNU/Linux. POSIX complient. Nutný znát v každém případě.[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/)

- `Zsh` - Interaktivní používání, silný skriptovací jazyk. POSIX complient. [https://www.zsh.org/](https://www.zsh.org/)

- `Fish` - Není POSIX, jde vlastní cestou. Inteligentní a uživatelsky přívětivý shell příkazového řádku. Fish provádí plnobarevné zvýraznění syntaxe příkazového řádku, stejně jako zvýraznění a dokončení příkazů a jejich argumentů, existence souboru a historie. Podporuje kompletní, jak píšete pro historii a příkazy. Fish je schopen analyzovat manuálové stránky systému, aby určil platné argumenty pro příkazy, což mu umožňuje zvýraznit a dokončit příkazy. Snadnou revizi posledního příkazu lze provést pomocí `Alt+Up` Pro další info [https://fishshell.com/](https://fishshell.com/)

# [](https://github.com/raven2cz/tux/tree/main/211112-shell-terminal#bash)

# Bash

Bash byl prezentován po celou dobu instalace a používání až do této nahrávky. Pro bash existuje bezpočet návodů, příkladů, psaní skriptů. Určitě doporučuji českou knihu pro shell [https://www.alza.cz/media/prikazovy-radek-v-linuxu-d2366810.htm](https://www.alza.cz/media/prikazovy-radek-v-linuxu-d2366810.htm) Dokumentace je zde [https://www.gnu.org/software/bash/manual/bash.html](https://www.gnu.org/software/bash/manual/bash.html)

# [](https://github.com/raven2cz/tux/tree/main/211112-shell-terminal#zsh)

# Zsh

## [](https://github.com/raven2cz/tux/tree/main/211112-shell-terminal#zsh-instalace)

## Zsh Instalace

My použijeme jako náš systémový shell ZSH.

```
sudo pacman -S zsh
chsh -s /usr/bin/zsh 
nvim ~/.zshrc
```

Použijeme [Oh My Zsh](https://ohmyz.sh/). Nebo [GitHub OhMyZsh](https://github.com/ohmyzsh/ohmyzsh).

```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## [](https://github.com/raven2cz/tux/tree/main/211112-shell-terminal#zsh-prompt-themes)

## Zsh Prompt Themes

```
# Change theme
ZSH_THEME="robbyrussell"
ZSH_THEME="agnoster"
ZSH_THEME="dst"
ZSH_THEME_RANDOM_CANDIDATES=(
  "robbyrussell"
  "agnoster"
  "dst"
)
# Need install p10k!
ZSH_THEME="powerlevel10k/powerlevel10k"
```

## [](https://github.com/raven2cz/tux/tree/main/211112-shell-terminal#instalace-zsh-plugins)

## Instalace Zsh plugins

```
plugins=(git zsh-autosuggestions zsh-syntax-highlighting z fzf sudo pass)

# Instalace plginu
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
#fzf
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
```

## [](https://github.com/raven2cz/tux/tree/main/211112-shell-terminal#instalace-colorscriptů)

## Instalace Colorscriptů

Colorscripty zkrášlují shell a uvozují danou instanci terminálu.

```
# DT Colorscript
git clone https://gitlab.com/dwt1/shell-color-scripts.git
makepkg -cf
sudo pacman -U *.pkg.tar.zst

# pokemon-colorscript
paru -S pokemon-colorscripts-git
```

# [](https://github.com/raven2cz/tux/tree/main/211112-shell-terminal#fish)

# Fish

Arch wiki [https://wiki.archlinux.org/title/Fish](https://wiki.archlinux.org/title/Fish)

## [](https://github.com/raven2cz/tux/tree/main/211112-shell-terminal#fish-instalace)

## Fish Instalace

```
sudo pacman -S fish
# plugin manager - nutno spoustet z fish shell
curl -sL https://git.io/fisher | source && fisher install jorgebucaran/fisher
fisher list
fisher update jorgebucaran/fisher
fisher remove jorgebucaran/nvm.fish@2.1.0
fisher list | fisher remove
# next useful scripts
paru -S lolcat exa fd bat timg p7zip glow
```

## STARSHIP Cross-Shell Prompt Instalace

Hlavní stránka [https://starship.rs/](https://starship.rs/)

```
sh -c "$(curl -fsSL https://starship.rs/install.sh)"
# add last line to your config.fish
starship init fish | source
```

### Personal Starship Settings

Moje osobní nastavení starship je v dotfiles uloženo v `~/.config/starship.toml` Toto moje nastavení nepoužívá dvě prompt řádky, ale pouze jednu, plus změnu symbolu. Nejprve zkuste defaultní nastavení a teprve potom můžete testovat tyto změny.

```
# Don't print a new line at the start of the prompt
add_newline = false

# Make prompt a single line instead of two lines
[line_break]
disabled = true

# Replace the "❯" symbol in the prompt with "➜"
[character]                         # The name of the module we are configuring is "character"
success_symbol = "[➜](bold green)"  # The "success_symbol" is set to "➜" with color "bold green"

# Use custom format
# format = """
# [┌───────────────────>](bold green)
# [│](bold green)$directory$rust$package
# [└─>](bold green) """

# Disable the package module, hiding it from the prompt completely
[package]
disabled = false
```

## Fish jako uživatelský interaktivní shell

Fish budeme používat jako **uživatelský interaktivní shell**, nikoliv jako systémový (pro init si ponecháme POSIX support). Do našeho `.zshrc` vložíme na konec toto

```
# jump from zsh to fish
if [[ $(ps --no-header --pid=$PPID --format=cmd) != "fish" ]]
then
	exec fish
fi
```

## [](https://github.com/raven2cz/tux/tree/main/211112-shell-terminal#fish-raven2cz-dotfiles)

## Fish Raven2cz Dotfiles

Zkopírujte fish adresář do `~/.config/fish` z raven2cz dotfiles.

```
nvim ~/.config/fish/config.fish
```

# [](https://github.com/raven2cz/tux/tree/main/211112-shell-terminal#důležité-odkazy)

https://www.youtube.com/watch?v=_K4ESyYuzE0

# Důležité odkazy

- [Youtube Channel TUX: Svět Linuxu](https://www.youtube.com/user/tondafischer/featured)

- [archlinux.org](https://archlinux.org/)

- [wiki.achlinux.org](https://wiki.archlinux.org/)

- [fishlive.org/blog](https://fishlive.org/en/blog-tech-art/arch)

- [github/raven2cz/tux](https://github.com/raven2cz/tux)

- [github/raven2cz/dotfiles](https://github.com/raven2cz/dotfiles)

- [Peertube kanál Arch Linux Cz](https://peertube.arch-linux.cz/w/dnyPyhvscq4bBRb6zNSNUk)