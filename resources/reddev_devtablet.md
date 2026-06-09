# REDDEV Development Tablet

## Overview

REDDEV Development Tablet is the central REDDEV in-game tablet for creator tools, administration tools, reports, weather controls, runtime pages, optional apps, and SQL/JSON persistence.

## Features

- REDDEV-styled tablet shell with app icons, wallpaper, scaling, theme, idle fade, and tablet animation support.
- Creator apps for blips, stashes, safezones, peds, and supported optional creator resources.
- Administration console with player tools, inventory tools, vehicle tools, reports, weather, resources, and activity history.
- Optional app ecosystem for REDDEV Music, Drug Creator, Garage Creator, Door Creator, and future REDDEV apps.
- Runtime tablet pages for player-facing menus.
- Framework-aware QBCore, Qbox, ESX, and standalone support.
- Inventory image path support for common inventories.
- Target support for ox_target, qb-target, and standalone floating text.
- SQL-first persistence with JSON fallback.
- Automatic and manual REDDEV unstuck cleanup.

## Dependencies

- No hard manifest dependency was found.
- `oxmysql` is recommended when `Config.Storage = 'sql'`.
- A supported framework is auto-detected or configured through `Config.Framework`.
- Optional target resources are auto-detected or configured through `Config.Target`.
- Optional weather resources checked include `qb-weathersync`, `Renewed-Weathersync`, `cd_easytime`, and `vSync`.
- Optional `screenshot-basic` is referenced by screenshot support in source scan.

## Installation

- Place `reddev_devtablet` in `resources/[Reddev-Scripts]/reddev_devtablet`.
- Add ACE permissions or configure framework groups for admin access.
- Add the `devtablet` item using `install/qbcore_item.lua` or `install/ox_inventory_item.lua` if players should open it from inventory.
- Copy `web/assets/items/devtablet.png` into your inventory image folder if needed.
- Import `install/reddev_devtablet.sql` for SQL persistence.
- Import `install/reddev_garage_system.sql` if using the complete REDDEV garage metadata system.

## Server.cfg Ensure Order

```cfg
ensure oxmysql
ensure reddev_devtablet
```

## Configuration

- `config.lua` controls debug, tablet item, open commands, framework, target, admin access, inventory image paths, weather resources, storage, garage metadata, safezone/ped/garage builder values, vehicle keys, tablet animation, and data files.
- `Config.Framework = 'auto'` supports auto, qbcore, qbox, esx, and standalone.
- `Config.Target = 'auto'` supports auto, ox_target, qb-target, and standalone.
- `Config.Storage = 'sql'` uses oxmysql when available and falls back to JSON.
- Data fallback files live under `data/*.json`.

## Commands

- `/devtablet` toggles the tablet.
- `/reddevtools` toggles the tablet.
- `/rddevtest` refreshes runtime data and opens the tablet for testing.
- `/noclip` toggles admin noclip through the admin shortcut path.
- `/reddevunstuck`, `/rdunstuck`, and `/reddevreset` release NUI focus, cameras, frozen movement, collision, invisible alpha, tasks, and disabled controls.
- `/staffchat` sends staff chat.
- `/a` sends staff chat.
- `/report` submits a player report.
- Key-mapped commands include `+reddev_tablet`, `+reddev_duty`, `+reddev_quick`, `+reddev_noclip`, `+reddev_waypoint`, `+reddev_heal`, `+reddev_revive`, and `+reddev_delete_vehicle`.

Public exports detected:

- `RegisterApp`
- `OpenRuntimeTabletPage`

Public/admin events detected:

- None documented as customer/admin entry points.

## Items

- `devtablet` is the default tablet item.
- Ready-to-paste item files are `install/qbcore_item.lua` and `install/ox_inventory_item.lua`.

## Permissions

- ACE admin access is enabled by `Config.AdminWithAce = true`.
- Detected ACE permissions include `reddev_admin.open`, `command`, `admin`, and `god`.
- Framework admin groups default to `admin`, `god`, and `mod`.
- Specific licenses can be whitelisted in `Config.AdminWithLicense`.
- Specific identifiers can be whitelisted in `Config.AdminWithIdentifier`.

## Inventory Support

- Inventory image paths are configured for `codem-inventory`, `ox_inventory`, `qb-inventory`, `lj-inventory`, `ps-inventory`, and `qs-inventory`.
- Source scan also detected `origen_inventory` references.

## Framework Support

- QBCore.
- Qbox.
- ESX.
- Standalone fallback.

## Target Support

- ox_target.
- qb-target.
- Standalone floating text.

## Database or SQL Setup

- SQL files: `install/reddev_devtablet.sql` and `install/reddev_garage_system.sql`.
- `Config.SqlTable` defaults to `reddev_devtablet_data`.
- `Config.GarageMetaTable` defaults to `reddev_garage_vehicle_meta`.
- `Config.GaragePrivateTable` defaults to `player_priv_garages`.
- When SQL is unavailable, the tablet falls back to JSON files under `data/`.

## Troubleshooting

- If admin tools are locked, confirm ACE permissions or `Config.AdminAllowedGroups`.
- If the tablet item does not open the UI, confirm `devtablet` exists in the active inventory item file.
- If data is not persisting, start `oxmysql` before `reddev_devtablet` or check JSON fallback files.
- If a player is stuck in NUI/camera/frozen state, run `/reddevunstuck`, `/rdunstuck`, or `/reddevreset`.
- If optional app icons are missing, confirm the optional resource is started and restart the tablet.

## FAQ

- **Do optional apps hard-crash when missing?** No. The plugin docs state optional apps hide when stopped or missing.
- **Can I run without SQL?** Yes, but SQL is recommended. JSON fallback is present.
- **How do other resources register apps?** Use `exports['reddev_devtablet']:RegisterApp({...})`.
