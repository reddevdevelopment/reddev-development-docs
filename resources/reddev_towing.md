# REDDEV Towing

## Overview

`reddev_towing` is a self-contained FiveM towing resource built around `flatbed3`, a physical hook-and-winch system, and a tow-remote interface. It can physically tow empty NPC vehicles and regular player-owned vehicles. Persistent impounding is optional and is currently integrated only with `qs-advancedgarages`.

The required `flatbed3` truck and `inm_flatbed_base` movable bed assets are bundled inside `reddev_towing`. Do not install or start a separate functional-flatbed resource.

## Requirements

The current `fxmanifest.lua` declares these dependencies:

- `ox_lib`
- `oxmysql`
- `interact-sound`

The live configuration also uses:

- QBCore through `qb-core`
- `ox_target`
- `qb-phone` for mission notifications
- The vehicle-key event `vehiclekeys:client:SetOwner`
- A framework/inventory item named `towremote`
- `qs-advancedgarages` only when persistent impounding is wanted

Physical towing continues to work when the persistent garage integration is disabled or unavailable.

### Bundled flatbed assets

Keep these model names unchanged:

- Tow truck: `flatbed3`
- Movable bed: `inm_flatbed_base`

The resource includes the required vehicle models, textures, bed object, archetype, handling, vehicle metadata, variations, colors, and vehicle-layout data. There is only one towing resource to start.

## Installation

1. Place the complete resource at `resources/reddev_towing`.
2. Keep the folder name `reddev_towing` and the model names `flatbed3` and `inm_flatbed_base`.
3. Import the bundled `player_tow_data.sql` through the database used by `oxmysql`. This table stores towing XP, completed jobs, earnings, and distance statistics.
4. Define `towremote` as a usable item in the active framework/inventory. The live QBCore item uses the image `towremote.png`.
5. Copy `ItemPNG/towremote.png` into the active inventory image directory.
6. Copy `InteractSoundFiles/flatbedsound.ogg` and `InteractSoundFiles/winchsound.ogg` into `interact-sound/client/html/sounds`.
7. Configure the framework, target, phone, key event, and garage mode in `config.lua`.
8. Start all dependencies and the optional garage resource before `reddev_towing`.

The active QBCore installation should follow this order:

```cfg
ensure oxmysql
ensure ox_lib
ensure qb-core
ensure interact-sound
ensure ox_target
ensure qb-phone
ensure qs-advancedgarages
ensure reddev_towing
```

If persistent impounding is disabled, the `qs-advancedgarages` line is not required by `reddev_towing`. Do not add a separate `flatbed3`, `inm_flatbed_base`, or old tow-job startup line.

After installation or configuration changes, restart the resource from the server console:

```text
restart reddev_towing
```

## Configuration

These examples match the current live `config.lua`:

```lua
Framework = "QBCore"
Config.CoreName = "qb-core"

Config.Target = "ox_target"
Config.Phone = "qb"
Config.VehicleKeysEvent = "vehiclekeys:client:SetOwner"

Config.TowVehicleModel = "flatbed3"
Config.AutomaticallHookVehicle = true
Config.MaxCableDistance = 15.0

Config.GarageSystem = "auto"
Config.AllowUnownedVehicleDisposal = true
```

The only supported `Config.GarageSystem` values are:

| Value | Behavior |
| --- | --- |
| `"auto"` | Detects a started, verified `qs-advancedgarages` resource. This is the live value. |
| `"qs-advancedgarages"` | Requires that exact resource to be started. |
| `"none"` | Disables persistent impounding while leaving physical towing available. |

The current persistent-impound settings are:

```lua
Config.Impound = {
    enabled = true,
    defaultReason = "Towed by authorized operator",
    defaultFee = 500,
    defaultDuration = 0,
    allowPayToRelease = true,
    requireTowJob = true,
    requireOnDuty = true,
    allowedJobs = {
        tow = true,
        police = true,
    },

    interactionDistance = 30.0,
    playerToTruckDistance = 15.0,
    truckToVehicleDistance = 12.0,
    bedToTruckDistance = 12.0,
    requestTimeout = 30000,
    cleanupDelay = 350,
    deleteFallbackDelay = 1500,
}
```

The default duration of `0` allows immediate paid release through the garage system. The default release fee is `$500`.

### Current road impound location

`reddev_towing` reads impound lots from the active QS configuration instead of duplicating them in its own config. The current valid road-vehicle lot is:

| Lot | Interaction coordinates | Vehicle release/spawn coordinates |
| --- | --- | --- |
| Hayes Autos | `vec3(483.75, -1312.29, 29.21)` | `vec4(493.279114, -1329.283569, 29.027100, 328.818909)` |

The flatbed, target vehicle, and operator must be within `30.0` metres of the configured road impound. The configured plane and boat impounds are not valid for road vehicles.

### Tow remote item

The usable item identifier is `towremote`. It is registered in `server/main.lua` and is also issued during the towing mission flow. The identifier is currently fixed in the resource rather than exposed as a separate config value.

## How to Tow a Vehicle

### Hook and winch procedure

1. Wait until the target vehicle is completely empty. The driver seat and every passenger seat must be free.
2. Position `flatbed3` in front of or behind the target vehicle and align the vehicle with the centre of the bed.
3. Lower the bed with the tow remote or `/toggletow` while sitting in `flatbed3`.
4. Exit the truck.
5. Walk to the rear hook and press `E` to collect it.
6. Walk to the front or rear bumper of the target vehicle and press `E` again to attach the cable.
7. Open the tow remote and hold the **Wind Hook** control to pull the vehicle onto the bed.
8. With `Config.AutomaticallHookVehicle = true`, keep the vehicle aligned and allow the automatic bed attachment to complete when it reaches the correct position.
9. Raise the bed before driving away.

The winch rejects the flatbed itself, occupied vehicles, invalid entities, and vehicles for which network control cannot be obtained.

### Quick attach

The remote can attach a vehicle without using the physical hook when all of these conditions are met:

- The bed is fully lowered.
- The vehicle is empty.
- The vehicle is centred at the rear of the bed.
- The vehicle is within approximately `3.7` metres of the flatbed hook point.

Select **ATTACH** on the tow remote. Use **DETACH** while the bed is lowered to remove an attached vehicle.

## Player-Owned Vehicle Support

Regular player-owned vehicles can be physically towed; towing is not limited to mission or NPC vehicles.

- The vehicle must be empty.
- Physical towing does not change ownership.
- Persistent impounding preserves the ownership record and plate.
- Saved vehicle properties, fuel, engine health, and body health are preserved during a successful QS impound.
- Vehicle keys are not transferred to the tow operator.

If the resource cannot obtain network control, the vehicle remains in place and the attach attempt is rejected.

## Persistent Impounding

To persistently impound a road vehicle:

1. Be on duty with the `tow` or `police` job.
2. Attach the empty vehicle to the bed of `flatbed3`.
3. Transport it to the valid QS road impound. On the current server, this is **Hayes Autos** at `vec3(483.75, -1312.29, 29.21)`.
4. Keep the loaded flatbed and your player within the configured `30.0`-metre interaction range.
5. Open the tow remote.
6. Select **IMPOUND**.

For a player-owned vehicle, the ownership record is updated and the vehicle becomes available through the QS impound UI with the configured `$500` release fee. For an NPC or otherwise unowned vehicle, the entity is disposed without creating an ownership record.

The **IMPOUND** button is available only when the supported garage integration is active, the operator is authorized and on duty, an empty vehicle is attached, and the loaded flatbed is at a valid road impound.

## QS Advanced Garages Integration

The current live server uses `qs-advancedgarages` version `5.0.20`. `Config.GarageSystem = "auto"` detects it when it is already started.

- The integration uses the existing QS exports and `player_vehicles` records.
- No QS resource files are modified by `reddev_towing`.
- The current QS setting remains `Config.ImpoundJobs = { 'police' }`.
- REDDEV Towing independently authorizes on-duty `tow` and `police` operators for its remote **IMPOUND** action.
- A successful owned-vehicle impound uses garage state `2`.
- The selected garage, depot price, impound data, vehicle properties, fuel, engine health, and body health are persisted.
- The owner/citizen identifier and plate are not replaced.
- The world entity is removed only after the persistence update succeeds.

If persistence fails or the record changes during the request, the operation fails safely and the vehicle is not deleted.

## NPC and Unowned Vehicles

NPC and other unowned vehicles can be physically towed and, with the live setting below, disposed at a valid QS road impound:

```lua
Config.AllowUnownedVehicleDisposal = true
```

No fake `player_vehicles` record is created. Setting this option to `false` prevents the persistent disposal of unowned vehicles; it does not disable ordinary physical towing.

## Permissions

The current authorization rules apply to persistent impounding:

- Allowed jobs: `tow` and `police`
- On-duty status: required
- Vehicle occupancy: every seat must be empty
- Valid road impound: required
- Server distance checks: player-to-truck `15.0` m, truck-to-vehicle `12.0` m, bed-to-truck `12.0` m, and impound interaction range `30.0` m
- Verified physical attachment to the correct `flatbed3` bed: required

The current physical hook, winch, and quick-attach controls are not job-gated by `Config.Impound.allowedJobs`; that table controls the persistent **IMPOUND** action.

## Network and Safety

The client sends network IDs for the tow truck, movable bed, and target vehicle. The server then checks the entities, entity types, `flatbed3` model, plate, saved model, player distance, lot distance, empty seats, and recorded physical attachment.

Duplicate requests for the same vehicle or plate are blocked. Invalid or stale entities are rejected. Pending request and tow-attachment state is cleared when it expires, when an entity disappears, when a player disconnects, or when the resource stops.

For player-owned vehicles, deletion is authorized only after the garage update succeeds. The client performs the normal cleanup, with a delayed server fallback if the client cannot complete it.

## Commands and Controls

| Command or control | Current behavior |
| --- | --- |
| `/toggletow` | While inside `flatbed3`, lowers or raises the bed. Raising is blocked while the hook is still attached to a vehicle. |
| `/towhook` | Outside a vehicle, collects, returns, drops, or attaches the hook. |
| `E` | Default key mapping for `/towhook`. Use it near the rear hook or a target bumper. It can be rebound in FiveM key settings. |
| Use `towremote` | Opens the draggable tow remote. |
| **Wind Hook** | Hold to wind the attached cable. |
| **Raise Bed / Lower Bed** | Moves the flatbed bed. |
| **ATTACH / DETACH** | Quick-attaches an eligible nearby vehicle or detaches a loaded vehicle. |
| **IMPOUND** | Sends an authorized persistent impound request at a valid road lot. |
| **REMOVE HOOK** | Removes the active hook/cable connection. |

There is no current default `G` key mapping for the bed and no separate `/impound` command. Use the tow remote or `/toggletow` for bed movement and the remote **IMPOUND** button for persistent impounding.

## Feature List

- Bundled `flatbed3` truck and `inm_flatbed_base` movable bed assets
- Physical hook, rope, and hold-to-wind winch
- Automatic bed attachment after winching
- Tow-remote bed, winch, attach, detach, hook-removal, and impound controls
- Quick attachment for centred empty vehicles within approximately `3.7` metres
- Physical towing of NPC and regular player-owned vehicles
- Empty-vehicle safety restriction
- Contract missions, payouts, towing XP, statistics, and 25 progression levels
- Automatic detection of `qs-advancedgarages`
- Persistent player-owned vehicle impounding through QS
- Optional NPC/unowned vehicle disposal without fake ownership records
- Independent on-duty `tow` and `police` authorization
- Ownership, plate, vehicle-property, fuel, engine, and body-state preservation
- Network ID validation, attachment validation, duplicate protection, and safe cleanup

## Troubleshooting

### Tow remote does not open

- Confirm the item name is exactly `towremote` and that it is usable in the active framework/inventory.
- Confirm `towremote.png` is installed in the inventory image directory.
- Check that `qb-core` and the inventory started before `reddev_towing`.
- Restart the framework/inventory after adding the item, then run `restart reddev_towing`.

### Hook cannot be picked up

- Fully lower the bed first; the internal bed state must be the lowered state.
- Exit the truck and stand near the rear hook. Pickup range is approximately `2.9` metres.
- Press `E` or run `/towhook`.
- If a stale rope is visible, use **REMOVE HOOK**, reposition the truck, and try again.

### Vehicle will not attach

- Make sure every seat is empty.
- Confirm the bed is fully lowered.
- For the winch, attach at the front or rear bumper and keep the cable within the configured `15.0`-metre maximum.
- For quick attach, centre the vehicle within approximately `3.7` metres of the hook point.
- If network control cannot be obtained, wait for the previous driver to exit and move away, then try again.

### Player-owned vehicle cannot be towed

Player-owned vehicles are supported. Check that the vehicle is empty, the bed is lowered, the vehicle is not the flatbed itself, and the client can obtain network control. Keys are not transferred to the operator.

### IMPOUND button is unavailable

- Confirm an empty vehicle is physically attached to the bed, not only connected to the rope.
- Confirm the operator has the `tow` or `police` job and is on duty.
- Confirm `Config.Impound.enabled = true`.
- Confirm the loaded flatbed is at the configured road impound and within `30.0` metres.
- Confirm `qs-advancedgarages` is active and detected.

### No supported garage detected

- Use only `"auto"`, `"qs-advancedgarages"`, or `"none"` for `Config.GarageSystem`.
- Start `qs-advancedgarages` before `reddev_towing`.
- Check the server console for the REDDEV Towing integration status line.
- Run `restart reddev_towing` after changing the mode or startup order.

### Vehicle does not appear in the QS impound UI

- Confirm the plate belongs to exactly one valid player-owned road-vehicle record.
- Confirm the entity plate and model match the saved record.
- Confirm the live QS road impound is configured as `isImpound = true` with `type = 'vehicle'`.
- Check the server console for a safe persistence rejection. The vehicle is intentionally kept when persistence is not confirmed.
- Confirm the player is checking the same QS impound lot recorded by the tow action.

### Occupied vehicle is rejected

This is intentional. The driver seat and all passenger seats must be empty before hook attachment, quick attachment, or persistent impounding.

### Changes do not take effect

Run:

```text
restart reddev_towing
```

If QS garage locations were changed, restart `qs-advancedgarages` first and then restart `reddev_towing` so the integration refreshes the active lots.

## Version

REDDEV Towing resource version: `1.0.0`.

QS Advanced Garages version verified on the current live server: `5.0.20`.
