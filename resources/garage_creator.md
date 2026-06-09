# Garage Creator

## Overview

REDDEV Garage Creator is a garage system and REDDEV tablet manager. It covers public, job, gang, private, and impound garages with vehicle storage, spawning, transfers, parking states, fees, and runtime tablet menus.

## Features

- Public, job, gang, private, and impound garages.
- Vehicle storage, spawning, transfers, parking states, return fees, and impound actions.
- Framework, keys, fuel, banking, target, and text prompt adapters.
- Vehicle image support through `vehicle_images/`.
- REDDEV Dev Tablet app registration using app id `garage_creator`.
- Tablet manager for garage locations and runtime settings.
- SQL install files for QBCore/Qbox and ESX.

## Dependencies

- `oxmysql`.
- `ox_lib`.
- OneSync and server build dependency from manifest.
- `reddev_devtablet` for tablet app registration and manager UI.
- A supported framework: QBCore, Qbox, or ESX.
- Optional configured integrations for fuel, keys, banking, gangs, draw text, target, and radial menu.

## Installation

- Place `garage_creator` beside `reddev_devtablet` in your REDDEV resources folder.
- Run `install/run-qb.sql` for QBCore/Qbox or `install/run-esx.sql` for ESX.
- Review `config/config.lua` for framework, fuel, vehicle keys, banking, target, garage locations, job/gang garages, impounds, and private garage settings.
- Optionally add custom PNG vehicle thumbnails to `vehicle_images/` and enable `Config.ShowVehicleImages`.
- Restart `garage_creator` and `reddev_devtablet` after install.

## Server.cfg Ensure Order

```cfg
ensure oxmysql
ensure ox_lib
ensure reddev_devtablet
ensure garage_creator
```

## Configuration

- `config/config.lua` controls framework, fuel, keys, notifications, banking, gangs, target, draw text, transfers, garage locations, job/gang garages, impounds, private garages, and admin commands.
- `config/config-cl.lua` and `config/config-sv.lua` contain client/server-specific config.
- `data/reddev_locations.json` stores tablet-managed garage overrides.
- `vehicle_images/README.md` documents custom vehicle image requirements.

## Commands

- `/garagecreator` opens the Garage Creator tablet manager.
- `/garage_creator` also opens the Garage Creator tablet manager.
- `/admincar` is registered for ESX admin vehicle handling.
- `/privategarages` opens the private garage list/create menu.
- `/setjobvehicle` assigns a vehicle to a job garage.
- `/removejobvehicle` removes a job garage vehicle assignment.
- `/setgangvehicle` assigns a vehicle to a gang garage.
- `/removegangvehicle` removes a gang garage vehicle assignment.
- `/iv` impounds a vehicle.
- `/vplate` opens vehicle plate change handling.
- `/dvdb` deletes a vehicle database record.
- `/vreturn` returns a vehicle plate to its garage.

Public exports detected:

- `getAllGarages`
- `impoundVehicle`
- `deleteOutsideVehicle`
- `registerVehicleOutside`

Public/admin events detected:

- `garage_creator:openTablet`

## Items

- No dedicated inventory items were found for basic install.
- Vehicle image files are optional UI assets, not inventory items.

## Permissions

- Job garage access uses configured jobs and minimum job grades.
- Gang garage access uses configured gangs and minimum gang grades.
- Private garage creation can be restricted by `Config.PrivGarageCreateJobRestriction`, defaulting to `realestate`.
- Several management commands are described as admin-only in config.

## Inventory Support

- No direct inventory item setup was found.

## Framework Support

- `Config.Framework = 'auto'` can detect or be forced to QBCore, Qbox, or ESX.
- QBCore/Qbox share the `install/run-qb.sql` setup path.
- ESX uses `install/run-esx.sql`.

## Target Support

- `Config.UseTarget` toggles target mode.
- `Config.Target` supports `ox_target` and `qb-target`.
- Floating text/draw text fallback is controlled through `Config.DrawText` and prompt settings.
- Standalone/interact references were detected for non-target prompts.

## Database or SQL Setup

- SQL files: `install/run-qb.sql` and `install/run-esx.sql`.
- The server includes `server/sv-initsql.lua`, but the install guide still tells admins to run the framework SQL file.
- Start `oxmysql` before this resource.

## Troubleshooting

- If the tablet icon does not appear, confirm `garage_creator` is started and restart `reddev_devtablet`.
- If vehicles do not save or spawn correctly, confirm the correct SQL file was run for your framework.
- If images do not show, confirm `Config.ShowVehicleImages = true` and that PNG files are in `vehicle_images/`.
- If gang garage behavior is missing on ESX, review `Config.GangEnableCustomESXIntegration`.

## FAQ

- **Do I create garages only in config?** The README says tablet-managed overrides save to `data/reddev_locations.json`, while original Lua configs remain in `config/`.
- **Which SQL should Qbox use?** Use `install/run-qb.sql`.
- **Does the tablet need manual app config?** No. The app registers itself and includes `data/tablet_app.json`.
