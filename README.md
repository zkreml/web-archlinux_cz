# 🐧 Arch Linux CZ — Komunitní web

Oficiální web české komunity Arch Linuxu — [arch-linux.cz](https://arch-linux.cz)

## Stack

- **Generátor:** [Hugo](https://gohugo.io/)
- **Téma:** [Hugo Blog Awesome](https://github.com/hugo-sid/hugo-blog-awesome)
- **Jazyk obsahu:** čeština
- **Hosting:** statický (nginx)

## Struktura

```
content/
├── posts/          # blogové články
├── navody/         # návody a tutoriály
├── zpravy/         # novinky z Arch světa
├── o-arch-linuxu.md
├── komunita.md
└── podporte-nas.md
```

## Lokální vývoj

```bash
# klonování s tématem
git clone --recurse-submodules ssh://git@git.arch-linux.cz:29418/ArchlinuxCz/web-archlinux_cz.git
cd web-archlinux_cz

# spuštění dev serveru
hugo server -D
```

## Build

```bash
hugo --minify
# výstup v public/
```

## Komunita

- [Wiki](https://wiki.arch-linux.cz)
- [Fórum](https://forum.arch-linux.cz)
- [Mastodon](https://mastodon.arch-linux.cz/@archlinux)
- [PeerTube](https://peertube.arch-linux.cz)
- [Matrix](https://matrix.to/#/#archlinuxcz:matrix.org)
- [Discord](https://discord.gg/sJYcCdENCT)

## Licence

Obsah © 2024–2026 Arch Linux CZ
