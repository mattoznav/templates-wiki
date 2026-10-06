# Wiki template

"Fieldbook", an unofficial reference for every Pokémon: a fast static website and a mobile app, both built on the free and open [PokéAPI](https://pokeapi.co/). It shows how to turn a large public API into a cross-linked reference: about 1,000 species with their forms, 900 moves, 300 abilities, 18 types and 30 games.

| Folder | What it is | Stack | Runs on |
| --- | --- | --- | --- |
| [`website`](website) | Static site with a page for every Pokémon, move, ability, type and generation, filters and instant search | Astro | `localhost:4323` |
| [`app`](app) | Mobile app with the same content, offline cache and saved Pokémon | Flutter | iOS and Android |

Live demo of the website: [mattoznav.github.io/templates-wiki-website](https://mattoznav.github.io/templates-wiki-website/), published from the website repository with GitHub Pages.

Each folder is a Git submodule with its own repository and its own README with more detail. There is no backend: the website reads PokéAPI once at build time, the app reads it directly and keeps what it reads on the device.

## Requirements

| Tool | Version | Needed for |
| --- | --- | --- |
| Git | any recent version | cloning the template with its submodules |
| Node.js and npm | Node 22.12 or newer | `website` |
| Flutter | 3.44 or newer | `app`, plus Xcode (iOS) or Android Studio (Android) |

An internet connection is needed the first time each part runs. No API key, account or database is needed.

## Install and run

### 1. Clone

```bash
git clone --recurse-submodules https://github.com/mattoznav/templates-wiki.git
cd templates-wiki
```

If you cloned without `--recurse-submodules`, run `git submodule update --init --recursive`.

### 2. Website

```bash
cd website
npm install
npm run dev
```

Open `http://localhost:4323`. The first run downloads the data from PokéAPI (about a minute) and caches it in `website/.cache/`; later runs start straight away. `npm run build` writes the static site to `website/dist/`.

### 3. App

Start an iOS simulator or an Android emulator, then from the repository root:

```bash
cd app
flutter pub get
flutter run
```

## How the two parts use PokéAPI

| | Website | App |
| --- | --- | --- |
| When | At build time | While the app is used |
| How | About 4,700 REST requests, cached on disk, reduced to compact JSON | One GraphQL query for every list, REST for each detail screen |
| Offline | The built site needs nothing from PokéAPI | Everything already opened is kept on the device |
| Images | Loaded from PokéAPI's sprite repository | Same, with an image cache |

Both follow PokéAPI's fair use policy, which asks clients to cache what they request.

## Credits and trademarks

Data from [PokéAPI](https://pokeapi.co/); artwork, sprites and cries are loaded from its public repositories and are not included here.

Pokémon and Pokémon character names are trademarks of Nintendo, Creatures Inc. and GAME FREAK inc. This template is an unofficial fan reference and is not affiliated with or endorsed by them.

## License

The code is released under the [MIT License](LICENSE). It covers the code only: data from PokéAPI, the artwork loaded from its repositories and the Pokémon trademarks are not covered.
