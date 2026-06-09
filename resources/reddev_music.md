# REDDEV Music

## Overview

REDDEV Music is an optional REDDEV Development Tablet addon for portable world audio, REDDEV tablet controls, and boombox placement powered by xSound.

## Features

- Optional REDDEV Dev Tablet app registration.
- Single `REDDEV Music` tablet app.
- Boombox item support for QBCore/Qbox, ox_inventory, and ESX setup examples.
- Portable speaker prop placement, pickup, removal, and distance cleanup.
- Vehicle playback mode when the boombox is used inside a vehicle.
- Player, vehicle, fixed-location, and boombox emitter modes.
- xSound world audio with volume and range controls.
- URL playback, saved tracks, queue, favorites, recent tracks, playlists, loop, and shuffle.
- YouTube metadata through oEmbed.
- Optional resolver endpoint for converting YouTube URLs to direct audio streams.

## Dependencies

- `xsound` is a manifest dependency.
- `reddev_devtablet` for optional tablet app display.
- `oxmysql` is loaded in server scripts for optional SQL-backed expansion.
- Streamed speaker prop `qua_jblspeaker`.

## Installation

- Place `reddev_music` beside `reddev_devtablet`.
- Start `xsound` before `reddev_music`.
- Add the `boombox` item to your inventory using `ITEMS.md`.
- Copy `reddev_music/items/boombox.png` into your inventory image folder.
- Review `config.lua` for framework, boombox model, categories, locale, and tablet resource name.
- Use `/reddevmusic` or the REDDEV tablet icon to test the app.

## Server.cfg Ensure Order

```cfg
ensure xsound
ensure reddev_devtablet
ensure reddev_music
```

## Configuration

- `config.lua` controls `ReddevMusic.boomboxModel`, `ReddevMusic.framework`, prompt beep behavior, music categories, language, locale strings, and `Config.TabletResource`.
- `Config.TabletResource` defaults to `reddev_devtablet`.
- `ITEMS.md` contains QBCore/Qbox, ox_inventory, and ESX item examples.
- `Config.ResolverEndpoint` is documented in README as the optional resolver hook, but no active assignment was found in `config.lua`.

## Commands

- `/reddevmusic` opens the REDDEV Music tablet app.
- The README/INSTALL mentions `/boombox`, but no `RegisterCommand('boombox')` was found in the scanned current source. Treat boombox as a usable item unless you add a command yourself.

Public exports detected:

- `Open`
- `GetSnapshot`

Public/admin events detected:

- None documented as customer/admin entry points.

## Items

- `boombox` is the portable speaker item.
- Image path: `reddev_music/items/boombox.png`.
- ox_inventory image target: `ox_inventory/web/images/boombox.png`.

## Permissions

- No ACE, job, gang, identifier, or admin group checks were found for basic use.
- Access is controlled by who has or receives the `boombox` item and who can access the tablet app.

## Inventory Support

- QBCore/Qbox item example in `ITEMS.md`.
- ox_inventory item example in `ITEMS.md`.
- ESX legacy SQL item example in `ITEMS.md`.
- README mentions qb-inventory, ox_inventory, and qs-inventory image folders.

## Framework Support

- `ReddevMusic.framework = 'qb'` by default.
- `ReddevMusic.framework = 'esx'` is documented as the other config option.
- Qbox can use the QBCore/Qbox item setup block, but no separate Qbox framework value was found.

## Target Support

- No target integration was found. Boombox world interaction uses key prompts.

## Database or SQL Setup

- SQL file: `install/reddev_music.sql`.
- The install guide says the current music library stores local player library state with resource KVP storage.
- The SQL file is described as optional tables and item snippets for future SQL-backed expansion.

## Troubleshooting

- If the app icon is missing, confirm `reddev_music` is started and restart `reddev_devtablet`.
- If music does not play, confirm `xsound` is started before `reddev_music`.
- If the item does not work, confirm the `boombox` item exists and its image was copied.
- If YouTube URLs fail, configure a resolver endpoint that returns the README's expected JSON contract.
- If `/boombox` does not work, the scanned code does not register that command; use the item or add a command.

## FAQ

- **Is REDDEV Music required for the tablet?** No. It is optional and the icon appears only while the resource is started.
- **Does it require xSound?** Yes. `xsound` is a manifest dependency.
- **Does it consume the boombox item?** Server code includes add/remove handlers for the `boombox` item; test your inventory path after setup.
