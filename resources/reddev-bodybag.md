# REDDEV Bodybag

## Overview

`reddev-bodybag` is a configurable bodybag and death-management resource for FiveM roleplay servers. It supports multiple bodybag item types, job restrictions, bodybag carrying, disposal zones, simulated afterlife teleporting, and optional permanent death flow.

## Features

- Multiple bodybag items configured in `Config.BodyBags`.
- Job whitelists and minimum grades per bodybag type.
- Simulated death flow to configurable Heaven/Hell coordinates.
- Optional permanent-death flow.
- Burial and cremation zones.
- Required disposal items and optional burning reward item.
- Target interactions for players, bodybags, and disposal zones.
- Command fallbacks for target-disabled servers.
- Bodybag cleanup when a player is revived.

## Dependencies

- QBCore/Qbox-style framework configured as `Config.Framework = 'qbcore'`.
- `qb-target` or `ox_target` when `Config.UseTarget = true`.
- Inventory item definitions and images for configured bodybag/disposal items.

## Installation

- Place `reddev-bodybag` in your server resources folder.
- Add configured bodybag items to your framework/inventory item file.
- Add required disposal items such as shovel, lighter, petrolcan, and optional reward item `deadopp` if you use the default config.
- Copy PNGs from `reddev-bodybag/item-images` into your inventory image folder.
- Edit `config.lua` for bodybag types, job access, target settings, afterlife locations, zones, and permanent death behavior.

## Server.cfg Ensure Order

```cfg
ensure qb-core
ensure reddev-bodybag
```

## Configuration

- `config.lua` controls framework, target mode, commands, target labels/icons, carrying blips, bodybag definitions, required disposal items, reward items, permanent death, afterlife points, and disposal zones.
- `locales/en.lua` contains player-facing messages.
- `install/op-multicharacter-reddev-bridge.lua` is present for multicharacter bridge support.

## Commands

- `/bodybag <type>` bags the closest dead/downed player. Default types include `standard`, `mafia`, and `permadeath`.
- `/unbodybag` opens/removes the closest bodybag.
- `/burybody` disposes at a burial zone.
- `/burnbody` disposes at a cremation/burning zone.
- `/carrybag` carries the closest bodybag.
- `/dropbag` drops the carried bodybag.

Public exports detected:

- `GetBodyBagByItem`

Public/admin events detected:

- None documented as customer/admin entry points.

## Items

- `bodybag` for the standard bag.
- `mafia_bodybag` for the mafia/cartel bag.
- `perma_bodybag` for the permanent-death bag.
- `shovel` required for burial by default.
- `lighter` and `petrolcan` required for burning by default.
- `deadopp` is the default burning reward item.

## Permissions

- `standard` bodybag has no job restriction by default.
- `mafia` bodybag allows `mafia` and `cartel` at grade 0+ by default.
- `permadeath` bodybag allows `ambulance` and `police` at grade 3+ by default.
- Disposal zones can also have job restrictions; defaults are unrestricted.

## Inventory Support

- QBCore-style item definitions are shown in the README.
- No ox_inventory-specific item block was found.

## Framework Support

- `Config.Framework = 'qbcore'` by default.
- Source scan also detected ESX references, but the visible config is QBCore-focused.

## Target Support

- `Config.TargetSystem = 'auto'` supports auto-detection.
- `qb-target` support detected.
- `ox_target` support detected.
- Commands remain available when target interactions are disabled.

## Database or SQL Setup

- No SQL files or database usage were found for the base resource.
- Permanent death may trigger the configured delete event `reddev-bodybag:forceDeleteCharacter`; integrate that event with your character system if you use permanent death.

## Troubleshooting

- If target options do not appear, confirm `Config.UseTarget = true` and that qb-target or ox_target is started.
- If a job cannot use a restricted bag, check the job name and minimum grade in `Config.BodyBags`.
- If disposal fails, confirm the player has the required disposal items.
- If permanent death should not happen, set `Config.PermanentDeath.Enabled = false` or avoid bags/zones using `mode = 'permanent'`.

## FAQ

- **Can any job use the standard bag?** Yes, default `standard.jobs = false`.
- **Does it need SQL?** No SQL setup was found.
- **Can I add more bag types?** Yes. Add another entry under `Config.BodyBags` and create the matching item.
