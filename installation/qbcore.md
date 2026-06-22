# QBCore Installation

## Overview

Use this page for QBCore servers installing the full REDDEV resource set.

## Base Ensure Order

```cfg
ensure qb-core
ensure oxmysql
ensure ox_lib
ensure xsound
ensure bob74_ipl
ensure screenshot-basic

ensure reddev_devtablet
ensure reddev_music
ensure drug_creator
ensure garage_creator
ensure doors_creator
ensure ammo_boxes
ensure reddev-bodybag
ensure vehicle_radio_disabler
ensure reddev_housecreator_props
ensure reddev_housecreator

ensure PolyZone
ensure qb-target
ensure qb-inventory
ensure reddev-shops
```

## SQL

- REDDEV Development Tablet: import `reddev_devtablet/install/reddev_devtablet.sql`.
- REDDEV garage metadata: import `reddev_devtablet/install/reddev_garage_system.sql` if using the REDDEV garage metadata system.
- Garage Creator: import `garage_creator/install/run-qb.sql`.
- Door Creator: run `doors_creator/sql/doors.sql` and `doors_creator/sql/doors_buildings.sql` if auto-creation is blocked.
- Drug Creator: import `drug_creator/sql/drug_creator.sql`.
- House Creator: run `[sql]/first_run_database_schema/reddev_housecreator_qb_all_in_one_RUN_FIRST.sql`.

## Items

- Add `devtablet` from `reddev_devtablet/install/qbcore_item.lua`.
- Add `boombox` from `reddev_music/ITEMS.md`.
- Add Drug Creator items from `drug_creator/ITEMS.md`.
- Add Ammo Boxes items from `ammo_boxes/install/items/items.lua`.
- Add Bodybag items from `reddev-bodybag/README.md`.
- Add House Creator items from `reddev_housecreator/[sql]/second_run_inventory_items/README_ITEMS.md`.
- For REDDEV Shops, make sure sellable items exist in `qb-core/shared/items.lua` or your active inventory item database. Keep `Config.HideMissingItems = true` to hide missing items from live shop menus.

## Permissions

```cfg
add_ace group.admin reddev_admin.open allow
add_ace group.admin reddev_admin.admin allow
add_ace group.admin doors_creator allow
add_ace group.admin reddev_door_creator allow
add_ace group.admin reddev-shops.admin allow
```

Also review each resource page for job/gang access settings.

## REDDEV Shops Notes

Only run `reddev-shops` for the unified shop system. Do not also run old shop, riddle, delivery, or `qb-shops` resources beside it.

Low-end servers can tune startup batching in `reddev-shops/config.lua`:

```lua
Config.Performance.spawnBatchSize = 1
Config.Performance.spawnBatchDelay = 200
Config.Performance.lazyPedSpawning = true
Config.Performance.lazyPedSpawnPerScan = 1
```

Random riddle ped movement, the arrival watermark, and riddle lazy ped spawning are configured in `reddev-shops/modules/riddles/config.lua`:

```lua
RiddleConfig.Performance.lazyPedSpawning = true
RiddleConfig.Performance.lazyPedSpawnPerScan = 1
RiddleConfig.Performance.lazyPedScanWait = 1500
```

Shop XP can be disabled for purchases in `reddev-shops/config.lua`:

```lua
Config.UseXpSystem = false
```

Players can view shop XP with `/xp`. The display uses a small REDDEV NUI card by default. Position, duration, accent color, and optional persistent watermark are configured under `Config.XpDisplay`.
