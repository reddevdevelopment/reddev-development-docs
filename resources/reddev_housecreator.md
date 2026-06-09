# REDDEV House Creator

## Overview

REDDEV House Creator is the housing addon for the REDDEV Development Tablet ecosystem. It includes house creation, house management, interiors, keys, doors, furniture, storage, wardrobes, garages, bills, rentals, property upgrades, and recovery commands.

## Features

- REDDEV tablet app integration for House Creator.
- House creation and house management.
- Shell/interior support with streamed props package.
- Keys, metakeys, doors, storage, wardrobes, garages, bills, rentals, and upgrades.
- Furniture and decoration workflows.
- Police breach/raid support through configured police jobs and storm ram item.
- Framework, inventory, wardrobe, garage, phone, dispatch, and target adapters.
- SQL install order for framework schema, inventory items, and optional house packs.
- Recovery commands for stuck housing UI/camera/decorating states.

## Dependencies

- `reddev_housecreator_props` must start before this resource.
- `ox_lib`.
- `bob74_ipl`.
- `screenshot-basic`.
- `oxmysql` through `@oxmysql/lib/MySQL.lua`.
- Manifest dependency `/assetpacks`.
- A supported framework adapter or standalone fallback.

## Installation

- Place `reddev_housecreator` in `resources/[Reddev-Scripts]/reddev_housecreator`.
- Install and start `reddev_housecreator_props` first.
- Run exactly one first-run database schema file for your framework.
- Add inventory items from `[sql]/second_run_inventory_items/README_ITEMS.md`.
- Optionally run one starter house location pack from `[sql]/third_optional_house_location_packs`.
- Review `config/main.lua`, `config/furniture.lua`, `config/webhooks.lua`, and `config/fivemanage.lua`.
- Restart props and House Creator, then test house creation, menus, doors, storage, wardrobe, garage, decorating, bills, and upgrades.

## Server.cfg Ensure Order

```cfg
ensure ox_lib
ensure bob74_ipl
ensure screenshot-basic
ensure oxmysql
ensure reddev_housecreator_props
ensure reddev_housecreator
```

## Configuration

- `config/main.lua` is the main setup file.
- `Config.Framework` auto-detects `es_extended`, `qb-core`, or `qbx_core`, otherwise falls back to standalone.
- `Config.Inventory` auto-detects supported inventory resources.
- `Config.UseTarget` toggles target interaction support.
- `Config.CreatorJobs` controls jobs allowed for creation/admin flows.
- `Config.PoliceJobs` defaults to `police` and `sheriff`.
- `config/furniture.lua` controls furniture data.
- `MORE_SHELLS.md` documents shell asset expectations.

## Commands

- `/housecreator` opens House Creator.
- `/houseMenu` and `/housemenu` open the house menu command path.
- `/realestate` opens the real estate menu.
- `/houseload` reloads/loads housing data.
- `/reddevhouseunstuck` and `/houseunstuck` run housing recovery cleanup.
- `/resetentrycoords` resets entry coordinates through the backwards shell module.
- `/revert_decorations` reverts decorations.
- `/housingfurniture` opens the furniture creator command from `Config.FurniCreatorCommand`.
- `/hireRenter` is configured as the renter command.
- `/gizmo`, `/take_offset`, and `/update_offset` are debug/setup commands.
- `Config.HouseBrowserCommand` is currently `true` while code registers that value as a command; confirm the intended command name before documenting it publicly.

Public exports detected:

- `TriggerServerCallback`
- `lockpick`
- `GetCurrentHouseData`
- `getHouseList`
- `getHouseData`
- `getCurrentHouse`
- `getEnteredHouse`
- `enterHouse`
- `GetClosestHouse`
- `GetCurrentHouseUpgrades`
- `getGarageShell`
- `inDecorate`
- `refreshCurrentDecorations`
- `initCurrentDecorations`
- `AddFurniture`
- `AddShell`
- `Scaleforms`
- `openApp`
- `openHouseCreator`
- `getTabletApp`
- `getShells`
- `RegisterServerCallback`
- `useHouseKey`
- `deleteHouse`
- `CheckHasKey`
- `GetPlayerHouses`
- `addDecorationToHouse`
- `CheckHasMetaKey`
- `GiveMetaKey`
- `RemoveMetaKey`

Public/admin events detected:

- None documented as customer/admin entry points.

## Items

- `housekey`.
- `lockpick`.
- `police_stormram`.
- `empty_weed_bag`.
- `weed_nutrition`.
- `weed_white-widow`, `weed_skunk`, `weed_purple-haze`, `weed_og-kush`, `weed_amnesia`, and `weed_ak47`.
- Matching weed seed items for the listed weed types.

## Permissions

- `Config.CreatorJobs` controls allowed creator jobs.
- `Config.PoliceJobs` defaults to `police` and `sheriff`.
- Framework admin checks use ACE `command` and framework group/job checks in custom framework adapters.
- House access uses key/metakey ownership and configured house data.

## Inventory Support

- `qs-inventory`.
- `qb-inventory`.
- `ps-inventory`.
- `ox_inventory`.
- `core_inventory`.
- `codem-inventory`.
- `inventory`.
- `origen_inventory`.
- `jaksam_inventory`.
- `tgiann-inventory`.
- `esx_inventory` adapters were also detected.

## Framework Support

- QBCore/Qbox through `qb-core` or `qbx_core` detection.
- ESX through `es_extended` detection.
- Standalone fallback.

## Target Support

- `qb-target` adapter file detected.
- `qtarget` and `ox_target` references detected.
- Non-target interaction fallback controlled by `Config.UseTarget = false` and interaction distances.

## Database or SQL Setup

- Run exactly one schema file first: `[sql]/first_run_database_schema/reddev_housecreator_qb_all_in_one_RUN_FIRST.sql` or `[sql]/first_run_database_schema/reddev_housecreator_esx_all_in_one_RUN_FIRST.sql`.
- Only run `[sql]/first_run_database_schema/optional_fresh_install_reset_RUN_BEFORE_FIRST_ONLY.sql` on a brand-new test database or when intentionally wiping old house data.
- Add items second using `[sql]/second_run_inventory_items/README_ITEMS.md`.
- Optionally run one location pack third: `optional_mirror_park_house_locations_RUN_THIRD.sql` or `optional_all_house_locations_RUN_THIRD.sql`.
- Do not run both optional location packs unless you understand the duplicate house-name/ID risk.

## Troubleshooting

- If shells or furniture are missing, confirm `reddev_housecreator_props` starts before `reddev_housecreator`.
- If SQL install fails, follow `[sql]/README_RUN_ORDER.md` and run only the correct framework schema.
- If players get stuck after housing UI/camera/decorating, use `/reddevhouseunstuck` or `/houseunstuck`.
- If police breach behavior does not work, confirm `police_stormram` exists and `Config.PoliceJobs` matches your server job names.
- If wardrobes or garages do not open, confirm the detected adapter matches your running resource.

## FAQ

- **Is game build 3095 required?** The README says startup no longer blocks build 2944, but 3095 is recommended for newest GTA asset compatibility.
- **Do props need a separate resource?** Yes. Start `reddev_housecreator_props` first.
- **Which SQL should Qbox use?** Use the QBCore/Qbox all-in-one file.
