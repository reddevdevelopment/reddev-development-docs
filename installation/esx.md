# ESX Installation

## Overview

Use this page for ESX Legacy-style servers. Some resources are QBCore-focused by default, so check each resource page before enabling everything.

## Base Ensure Order

```cfg
ensure es_extended
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
ensure vehicle_radio_disabler
ensure reddev_housecreator_props
ensure reddev_housecreator
```

## SQL

- REDDEV Development Tablet: import `reddev_devtablet/install/reddev_devtablet.sql`.
- REDDEV garage metadata: import `reddev_devtablet/install/reddev_garage_system.sql` if using the REDDEV garage metadata system.
- Garage Creator: import `garage_creator/install/run-esx.sql`.
- Door Creator: run `doors_creator/sql/doors.sql` and `doors_creator/sql/doors_buildings.sql` if auto-creation is blocked.
- Drug Creator: import `drug_creator/sql/drug_creator.sql`.
- House Creator: run `[sql]/first_run_database_schema/reddev_housecreator_esx_all_in_one_RUN_FIRST.sql`.
- Music and Drug Creator item guides include ESX item SQL examples.

## Configuration Notes

- `reddev_devtablet` supports `Config.Framework = 'auto'` or `esx`.
- `garage_creator` supports ESX in `Config.Framework`.
- `reddev_housecreator` detects `es_extended`.
- `reddev_music` supports `ReddevMusic.framework = 'esx'`.
- `drug_creator` supports `Config.Framework = 'esx'`.
- `ammo_boxes` and the visible bodybag config are QBCore-focused; review before using them on ESX.
