---
title: "Jak opravit poškozený soubor historie zsh"
date: 2022-11-04
author: "archos"
draft: false
categories: ['Návody']
tags: ['zsh']
---

Občas můžete zjistit, že máte poškozený soubor historie zsh, který vám brání v použití příkazu `fc` nebo v prohledávání historie. Zde je návod, jak to opravit.

### Poškozený soubor historie ZSH

Pokud použijete [`zsh`](http://www.zsh.org/) pro váš shell, velmi příležitostně můžete najít následující zprávu, která označuje poškozený soubor historie. To je obvykle po restartu.

```
zsh: corrupt history file /home/george/.zsh_history
```

Tím se zabrání vyhledávání zpět v historii pomocí `CTRL+R` a editaci předchozích příkazů pomocí [`fc`](https://shapeshed.com/unix-fc/).

### Jak to opravit

Chcete-li to opravit, spusťte následující příkazy

```
cd ~
mv .zsh_history .zsh_history_bad
strings -eS .zsh_history_bad > .zsh_history
fc -R .zsh_history
```

[zdroj](https://shapeshed.com/zsh-corrupt-history-file/)