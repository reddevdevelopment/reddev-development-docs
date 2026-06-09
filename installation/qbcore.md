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

## Permissions

```cfg
add_ace group.admin reddev_admin.open allow
add_ace group.admin reddev_admin.admin allow
add_ace group.admin doors_creator allow
add_ace group.admin reddev_door_creator allow
```

Also review each resource page for job/gang access settings.
