# Door Creator

## Overview

REDDEV Door Creator is a tablet-integrated door management addon. It lets approved staff create, edit, delete, lock, unlock, import, and sync doors from the REDDEV Development Tablet.

## Features

- Registers as a REDDEV Dev Tablet app with app id `door_creator`.
- Door list, create, edit, delete, lock, and unlock workflows.
- Single door and double door setup.
- Job, gang, identifier, item, and grade permission support where configured.
- Interaction distance, lockpick, sounds, icon, automatic door, and time-rule settings.
- Database-backed door and building tables.
- Door state sync to players.
- Optional import support for existing `qb-doorlock` doors.

## Dependencies

- `ox_lib` through `@ox_lib/init.lua`.
- `oxmysql` through `@oxmysql/lib/MySQL.lua`.
- OneSync is required by manifest dependency `/onesync`.
- A framework resource before Door Creator.
- `reddev_devtablet` before Door Creator for tablet app registration.
- `qb-doorlock` only if you want to import existing qb-doorlock doors.

## Installation

- Place `doors_creator` in `resources/[Reddev-Scripts]/doors_creator`.
- Confirm the tablet icon exists at `reddev_devtablet/html/assets/door_creator.png`.
- Start framework, database, `ox_lib`, and `reddev_devtablet` before this resource.
- Run `sql/doors.sql` and `sql/doors_buildings.sql` manually if your database user cannot auto-create tables.
- Grant admin ACE permissions before testing the tablet app.
- For qb-doorlock import, add the documented `exports('getConfig', function() return Config end)` to `qb-doorlock/config.lua` and restart qb-doorlock.

## Server.cfg Ensure Order

```cfg
ensure ox_lib
ensure oxmysql
ensure reddev_devtablet
ensure doors_creator
```

## Configuration

- `current_config.json` contains active settings such as locale, modules, lockpick item, target mode, keybind, ACE permission, lockpick police/quantity settings, and save-door-state behavior.
- `utils/settings/default_config.json` contains the default settings template.
- The README states `config.acePermission` is currently `doors_creator`.
- Module folders under `_modules/` provide logs, progress bar, dispatch, lockpick, text UI, and gang integrations.

## Commands

- `/doorscreator` opens the creator for authorized staff.
- `/togglelock` toggles the closest configured door.
- `/getClosestDoor` prints or fetches the closest door information for setup/debugging.
- `/_police_debug_doors_creator` is registered by the police debug module and should be treated as an internal/debug command.

Public exports detected:

- `toggleIconDisplay`
- `getDoorIdFromEntity`
- `getClosestActiveDoor`
- `getClosestDoorObjectFromDoorsId`
- `getAllDoors`
- `getConfig`
- `createBuilding`
- `getDoorIdData`
- `getBuildingIdData`
- `setDoorState`
- `registerShopInDoorsId`
- `unregisterShopIdFromDoors`
- `createDoor`
- `deleteDoor`
- `updateDoor`
- `getAllBuildings`
- `refreshDatabase`
- `replaceShowHelpNotification`
- `disableScriptEvent`

Public/admin events detected:

- `doors_creator:openTablet`

## Items

- `lockpick` is configured as the lockpick item in `current_config.json`.
- Door-specific item requirements can be configured per door; no standalone item definition file was found.

## Permissions

- Admin access uses ACE permission `doors_creator` by default.
- Install guide grants `doors_creator` and `reddev_door_creator` to `group.admin`.
- Door access supports jobs, gangs, identifiers, items, and grade checks where configured on doors.
- Detected identifier-style support includes license, license2, and steam identifiers.

## Inventory Support

- `ox_inventory` support was detected.
- Item checks are used for door/item restrictions and lockpick behavior.

## Framework Support

- QBCore and ESX framework support were detected through framework utilities.

## Target Support

- `ox_target` support detected.
- `qb-target` support detected.
- Standalone/no-target interaction settings are available through config.
- `interact` support was also detected in source references.

## Database or SQL Setup

- SQL files: `sql/doors.sql` and `sql/doors_buildings.sql`.
- The README says the resource can run these automatically and can add newer missing columns at startup.
- If auto creation is blocked by database permissions, run the SQL files manually in the listed order.

## Troubleshooting

- If the app icon is missing, confirm `doors_creator` is started and restart `reddev_devtablet`.
- If staff get no permission, confirm the admin group has `doors_creator` or `reddev_door_creator` ACE access.
- If SQL errors appear, confirm `oxmysql` starts before `doors_creator` and manually import the SQL if needed.
- If imported qb-doorlock doors are missing, confirm `qb-doorlock/config.lua` exposes `getConfig` and restart qb-doorlock first.

## FAQ

- **Do I need to edit the tablet config?** No. The Door Creator README says the app registers automatically.
- **Can I import qb-doorlock doors?** Yes, if qb-doorlock exposes its config through the documented export.
- **What permission should admins receive?** Use `add_ace group.admin doors_creator allow` and optionally `reddev_door_creator`.
