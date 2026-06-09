# Drug Creator

## Overview

REDDEV Drug Creator is a drug runtime and creator addon with tablet integration. The scanned config includes planting, plants, zones, selling, shops, bagging, cooking stations, equipment, effects, access, image paths, and item setup.

## Features

- Registers as a REDDEV Dev Tablet app with app id `drug_creator`.
- Config-driven plants, disabled placement areas, selling behavior, shops, equipment stations, and recipes.
- Equipment types include bagging, cauldron, oven, mixer, press, and cooking tables.
- Police job checks and minimum-police selling logic were detected.
- Floating prompt deconflict settings are included for target/eye overlap prevention.
- Item setup guide includes QBCore/Qbox, ox_inventory, and ESX item examples.

## Dependencies

- `ox_lib` through `@ox_lib/init.lua`.
- `mysql-async` through `@mysql-async/lib/MySQL.lua`.
- Manifest dependency `/assetpacks`.
- Framework adapter configured by `Config.Framework`.
- Inventory adapter configured by `Config.Inventory`.
- Target adapter configured by `Config.Target`.
- `reddev_devtablet` for optional app registration.

## Installation

- Place `drug_creator` in `resources/[Reddev-Scripts]/drug_creator`.
- Import `sql/drug_creator.sql` before testing database-backed data.
- Add the item definitions from `ITEMS.md` to your active inventory/framework item system.
- Copy item images from `drug_creator/inventory_images/` into your inventory image folder.
- Edit `config.lua` for framework, inventory, target, access, recipes, plants, zones, selling, shop, and equipment settings.

## Server.cfg Ensure Order

```cfg
ensure ox_lib
ensure mysql-async
ensure reddev_devtablet
ensure drug_creator
```

## Configuration

- `config.lua` is the main configuration file.
- `Config.Framework` defaults to `qb` and documents `qb`, `qbox`, and `esx` examples.
- `Config.Inventory` defaults to `qb` and documents `qb`, `ox`, and `qs` examples.
- `Config.Target` defaults to `qb` and documents `qb` and `ox` examples.
- `Config.UseTarget` controls whether selling/interactions use target options or floating prompts.
- `Config.Access.allowedJobs`, `Config.Access.requireAdmin`, and `Config.AdminGroups` control creator/admin access.
- `data/config_backup.lua` is written before saves from the tablet config editor.

## Commands

- `/drugcreator` opens the Drug Creator guide/menu based on `Config.Tablet.command`.

Public exports detected:

- `openDrugCreator`
- `openApp`
- `getDrugCreatorApp`
- `getTabletApp`
- `setZoneBucket`

Public/admin events detected:

- `drug_creator:openTablet`

## Items

- `acid`
- `bagged_meth`
- `bagged_weed`
- `bagging_table`
- `baggy`
- `cannabis_seed`
- `cauldron`
- `coca_leaf`
- `coca_seed`
- `cocaine`
- `coke_base`
- `coke_brick`
- `coke_oven`
- `default_lamp`
- `explosive_meth`
- `fertilizer`
- `gasoline`
- `liquid_meth`
- `meth`
- `meth_cooking_table`
- `meth_oven`
- `mixer`
- `phos`
- `plant_pot`
- `press`
- `pseudo`
- `water_bottle`
- `weed`

## Permissions

- `Config.Access.allowedJobs` can restrict creator/admin UI by job.
- `Config.Access.requireAdmin` can require admin/group access.
- `Config.AdminGroups` includes `admin`, `god`, and `superadmin` by default.
- `Config.PoliceJobs` includes `police` and `sheriff` by default for police-count logic.

## Inventory Support

- `qb` inventory adapter.
- `ox` inventory adapter.
- `qs` inventory adapter.
- The item guide also includes QBCore/Qbox, ox_inventory, and ESX item setup examples.

## Framework Support

- `qb` framework adapter.
- `qbox` is documented as a framework example in config.
- `esx` framework adapter.

## Target Support

- `qb` target adapter maps to qb-target.
- `ox` target adapter maps to ox_target.
- `none`/floating text behavior is supported through `Config.UseTarget = false` or target settings.

## Database or SQL Setup

- SQL file: `sql/drug_creator.sql`.
- Manifest loads `@mysql-async/lib/MySQL.lua`.
- oxmysql references were also detected in source, but the manifest points at mysql-async.

## Troubleshooting

- If the tablet app does not appear, confirm `drug_creator` and `reddev_devtablet` are both started.
- If items do not work, confirm every item from `ITEMS.md` exists and images were copied.
- If target prompts do not appear, confirm `Config.Target`, `Config.UseTarget`, and your target resource match.
- If creator access is too open, set `Config.Access.requireAdmin = true` or add job restrictions.

## FAQ

- **Is there a full README?** No README/INSTALL file was found; this page is based on `ITEMS.md`, `config.lua`, SQL, manifests, and source patterns.
- **Can I use ox_inventory?** Yes. `ITEMS.md` includes ox_inventory definitions and code checks for `Config.Inventory = 'ox'`.
- **Does it register with the REDDEV tablet?** Yes. The app metadata uses `drug_creator:openTablet`.
