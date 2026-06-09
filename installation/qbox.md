# Qbox Installation

## Overview

Qbox installs are closest to the QBCore path. Use QBCore/Qbox item blocks where the resource provides shared item examples.

## Base Ensure Order

```cfg
ensure qbx_core
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
- Garage Creator: use `garage_creator/install/run-qb.sql`.
- Door Creator: run `doors_creator/sql/doors.sql` and `doors_creator/sql/doors_buildings.sql` if auto-creation is blocked.
- Drug Creator: import `drug_creator/sql/drug_creator.sql`.
- House Creator: use `[sql]/first_run_database_schema/reddev_housecreator_qb_all_in_one_RUN_FIRST.sql`.

## Configuration Notes

- `reddev_devtablet` supports `Config.Framework = 'auto'` or `qbox`.
- `garage_creator` supports Qbox in `Config.Framework`.
- `reddev_housecreator` detects `qbx_core` and maps it to the internal QB adapter.
- Drug Creator config documents `qbox` as a framework example.

## Items

Use the QBCore/Qbox item examples from the resource docs unless your Qbox inventory expects ox_inventory definitions.
