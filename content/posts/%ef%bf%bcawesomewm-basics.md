---
title: "￼AwesomeWM Basics"
date: 2022-04-17
author: "archos"
draft: false
categories: ['Návody']
tags: ['awesome']
series: ['Arch Linux instalace']
---

AwesomeWM patří k nejlepším window managerům s podporou vyššího programovacího jazyka Lua. Ukážeme si, proč tento WM má takový význam a jeho nesporné výhody. Naučíme se jej nainstalovat, nastavit základní témata a testovat svá nastavení v testovacím prostředí. Nakonec vyzkoušíme základní ovládání a nápovědu klávesových zkratek. Součástí nahrávky je rovněž velmi jemný úvod do programovacího jazyka Lua. Další díl seriálu [Tondy Fischera.](https://github.com/raven2cz)

![](https://arch-linux.cz/wp-content/uploads/2022/04/awesomewm-1-1024x576.jpg)

![](https://arch-linux.cz/wp-content/uploads/2022/04/awesomewm-2-1024x576.jpg)

## [](https://github.com/raven2cz/tux/tree/main/211205-awesome-basics#awesome-window-manager)Awesome Window Manager

`Awesome` je vysoce konfigurovatelný správce oken nové generace pro Xorg. Je velmi rychlý a rozšiřitelný pomocí perfektně zdokumentovaného API. Primárně se zaměřuje na pokročilé uživatele, vývojáře a všechny lidi, kteří se zabývají každodenními složitějšími úkoly a chtějí mít plnou kontrolu nad ovládáním jejich **vlastního grafického prostředí**.

- Základní stránka: [https://awesomewm.org/](https://awesomewm.org/)- Arch Wiki: [https://wiki.archlinux.org/title/Awesome](https://wiki.archlinux.org/title/Awesome)- Screenshot Gallery: [https://mipmip.github.io/awesomewm-screenshots/](https://mipmip.github.io/awesomewm-screenshots/)- API Dokumentace: [https://awesomewm.org/apidoc/](https://awesomewm.org/apidoc/)- Ukázka mého ricing YouTube nahrávka: [Awesome není pouze Tiling Window Manager](https://youtu.be/-Fo7mB6_Wtg)

## LUA - Programovací jazyk

![](https://arch-linux.cz/wp-content/uploads/2022/04/lua-info.png)*Lua *

- Základní web: [https://www.lua.org/](https://www.lua.org/), [https://www.lua.org/start.html](https://www.lua.org/start.html)- Vynikající kniha (nutno přečíst): [https://www.lua.org/pil/](https://www.lua.org/pil/)- **Programming in Lua, fourth edition**

## Lua Wiki Info

**Lua** je odlehčený, reflexivní, imperativní a procedurální programovací jazyk navržený jako skriptovací jazyk s rozšiřitelnou sémantikou. Název je odvozen z portugalského slova pro měsíc.

Jazyk Lua je určen jako rozšiřující nebo skriptovací jazyk a je dostatečně malý, aby se vešel na nejrůznější hostitelské platformy. Podporuje jen malé množství atomárních datových struktur jako jsou boolovské hodnoty, čísla (implicitně s dvojitou přesností plovoucí čárky) a řetězce. Běžné datové struktury jako jsou pole, množiny, hashovací tabulky, seznamy a záznamy mohou být reprezentovány použitím jediné nativní datové struktury – tabulky, která je v podstatě heterogenním asociativním polem. Jmenné prostory a objekty mohou být vytvořeny taktéž za použití tabulek. Zahrnutím minimálního počtu datových typů se Lua pokouší dosáhnout rovnováhy mezi sílou a velikostí.

Sémantika Lua může být rozšiřována a měněna předefinováním některých zabudovaných funkcí v metatabulkách. Navíc podporuje Lua pokročilé vlastnosti, jako jsou funkce vyššího řádu a garbage collector. Kombinací mnoha těchto vlastností je možné v Lua psát i objektově orientované programy.

Lua se uplatňuje především v mnoha hrách, jako je **World of Warcraft**, masivní onlinová multiplayerová hra na hrdiny, ve které si mohou uživatelé přizpůsobit uživatelské rozhraní, animace postav a vzhled světa právě v jazyku Lua, a sérii Baldur’s Gate a videohře MDK2, kde je použit jako skriptovací jazyk pro moduly. Také se objevuje v některých open source hrách, jakými jsou Battle for Wesnoth, Daimonin a hry ve stylu Rogue: ToME a H-World. Skripty v jazyce Lua jsou také využity u her Worms 3D, Worms 4: Mayhem, Mafia II a v modifikaci pro GTA V, FiveM. Therescript, použitý k řízení vozidel a animací v There, je mírně upravená verze Lua. Správce oken Ion používá Lua pro své přizpůsobování a rozšiřování. Program Chat Mapper pro zapisování a ukládání rozhovorů (například mezi postavami ve hrách) používá jazyk Lua k řízení rozhovoru. Program LuaTeX rozšiřuje primitivní příkazy TeXu o možnost zadávání kódu v jazyce Lua.

V našem případě budeme Lua používat pro `AwesomeWM` a `Neovim`.

## The Eight-Queen in Programming in Lua Fourth Edition (8 královen z knihy programování Lua 4. vydání)

```
N = 8 -- board size

-- check whether position (n, c) is free from attacks
function isplaceok (a, n ,c)
    for i = 1, n - 1 do -- for each queen already placed
        if (a[i] == c) or           -- same column?
        (a[i] - i == c - n) or      -- same diagonal?
        (a[i] + i == c + n) then    -- same diagonal?
            return false -- place can be attacked
        end
    end
    return true -- no attacks; place is OK
end

-- print a board
function printsolution (a)
    for i = 1, N do                 -- for each row
        for j = 1, N do             -- and for each column
            -- write "X" or "-" plus a space
            io.write(a[i] == j and "X" or "-", " ")
        end
        io.write("\n")
    end
    io.write("\n")
end

-- add to board 'a' all queens from 'n' to 'N'
function addqueen (a, n)
    if n > N then -- all queens have been placed?
        printsolution(a)
    else -- try to place n-th queen
        for c = 1, N do
            if isplaceok(a, n, c) then
                a[n] = c -- place n-th queen at column 'c'
                addqueen(a, n + 1)
            end
        end
    end
end

-- run the program
addqueen({}, 1)
```

## Awesome základní instalace

```
paru -S awesome-git
mkdir -p ~/.config/awesome
cp /etc/xdg/awesome/rc.lua ~/.config/awesome/
nvim ~/.xinitrc
```

## Awesome základní konfigurace před spuštěním

Editujte `~/.config/awesome/rc.lua` Zkopírujte požadované themes do vašeho prostředí: `/usr/share/awesome/themes/ Copy it to ~/.config/awesome/themes/`

```
-- theme examples: default, zenburn
-- beautiful.init(gears.filesystem.get_configuration_dir() .. "/themes/default/theme.lua")
local theme_path = string.format("%s/.config/awesome/themes/%s/theme.lua", os.getenv("HOME"), "default")
beautiful.init(theme_path)
-- terminal and editor settings
terminal = "kitty"
editor = os.getenv("EDITOR") or "nvim"
```

## Ověření a testování AwesomeWW Sandbox

Použijeme Xephyr pro testování Xorg.

```
paru -S xorg-server-xephyr
Xephyr :1 -ac -br -noreset -screen 1980x1024 &
DISPLAY=:1.0 awesome -c ~/.config/awesome/rc.lua
```

Volitlně použít wrapper: `awmtt` (Awesome WM Testing Tool) z AUR

## Defaultní ovládání awesome (AwesomeWM Default Keybindings)

![](https://arch-linux.cz/wp-content/uploads/2022/04/awesome-keybindings-default-1024x684.png)***awesome-keybindings-defaul**t*

## Defaultní rc.lua

Pojďme si projít základní sekce a organizaci `nvim ~/.config/awesome/rc.lua`

https://www.youtube.com/watch?v=wi_EM5zXt8s&t=112s

# Důležité odkazy

- [Youtube Channel TUX: Svět Linuxu](https://www.youtube.com/user/tondafischer/featured)- [archlinux.org](https://archlinux.org/)- [wiki.achlinux.org](https://wiki.archlinux.org/)- [fishlive.org/blog](https://fishlive.org/en/blog-tech-art/arch)- [github/raven2cz/tux](https://github.com/raven2cz/tux)- [github/raven2cz/dotfiles](https://github.com/raven2cz/dotfiles)