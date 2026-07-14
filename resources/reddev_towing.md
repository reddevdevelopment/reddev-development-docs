# REDDEV Towing

## Overview

`reddev_towing` is a professional towing-job resource for FiveM with an interactive flatbed, working bed and winch controls, contract missions, configurable payouts, and persistent driver progression.

The required `flatbed3` vehicle and `inm_flatbed_base` bed object are bundled inside the resource. Do not install or start a separate functional-flatbed resource.

## Features

- Complete pickup, loading, delivery, unloading, and job-completion flow.
- Bundled `flatbed3` vehicle and `inm_flatbed_base` movable bed assets.
- Raise/lower controls with movement and hook safety checks.
- Winch rope, hook attachment, automatic vehicle attachment option, and cable-distance cleanup.
- Draggable tow-remote NUI supplied through the `towremote` inventory item.
- Contract pricing, refundable truck deposit, and configurable XP rewards.
- 25 configurable progression levels with payout multipliers and rewards.
- Persistent jobs, earnings, distance, and towing XP statistics.
- QBCore and ESX framework adapters.
- `qb-target` and `ox_target` support.
- Phone notifications for qb-phone/Renewed Phone, Quasar Smartphone, LB Phone, and YSeries.
- Configurable vehicle-key event.

## Included flatbed assets

The following model identifiers must remain unchanged:

- Tow vehicle: `flatbed3`
- Movable bed object: `inm_flatbed_base`

The resource includes the vehicle models, textures, object model, archetype definition, handling data, vehicle metadata, variations, colors, and vehicle-layout metadata. Only one `fxmanifest.lua` and one resource startup line are required.

## Dependencies

Required by the current manifest:

- `ox_lib`
- `oxmysql`
- `interact-sound`
- QBCore (`qb-core`) or ESX (`es_extended`)
- `qb-target` or `ox_target`
- A compatible inventory containing the `towremote` item

Integration dependencies:

- A supported phone resource when mission emails are enabled.
- Your configured vehicle-key resource/event.

## Installation

1. Place the complete folder in your resources directory as `reddev_towing`.
2. Do not rename the folder, `flatbed3`, or `inm_flatbed_base`.
3. Import `player_tow_data.sql` into the database used by `oxmysql`.
4. Add the `towremote` item to the active framework/inventory item definitions.
5. Copy `ItemPNG/towremote.png` into the active inventory image directory.
6. Copy `InteractSoundFiles/flatbedsound.ogg` and `InteractSoundFiles/winchsound.ogg` into the active `interact-sound/client/html/sounds` directory.
7. Configure the framework, target, phone, and vehicle-key settings in `config.lua`.
8. Start the dependencies before `reddev_towing`.

### Startup order

Use only one towing-resource startup entry. A typical QBCore order is:

```cfg
ensure oxmysql
ensure ox_lib
ensure interact-sound
ensure qb-core
ensure ox_target
ensure qb-phone
ensure reddev_towing
```

Replace the target and phone resource names with the integrations used by your server. Do not add `ensure vd-towjob`, `ensure flatbed3`, or a separate functional-flatbed ensure line.

## Tow remote item

### QBCore

Add the following entry to `qb-core/shared/items.lua` if the item does not already exist:

```lua
['towremote'] = {
    name = 'towremote',
    label = 'Tow Remote',
    weight = 100,
    type = 'item',
    image = 'towremote.png',
    unique = false,
    useable = true,
    shouldClose = true,
    combinable = nil,
    description = 'Remote control for the tow truck'
},
```

If `ox_inventory` imports QBCore shared items, define the item only once in the QBCore file. Otherwise add an equivalent `towremote` definition to the inventory's own item data file.

### ESX

Create a usable item named `towremote` in the item system used by your ESX server and install `towremote.png` in the matching inventory image directory.

## Database

Import the supplied file:

```text
player_tow_data.sql
```

It creates the `player_tow_data` table used for:

- Towing XP
- Completed-job count
- Total earnings
- Total towing distance
- Created and updated timestamps

The player citizen/character identifier is stored in `citizenid`.

## Configuration

The main options are in `config.lua`.

### Framework

```lua
Framework = "QBCore" -- or "ESX"
Config.CoreName = "qb-core"
```

For ESX, use `Framework = "ESX"` and set `Config.CoreName` to the name of the active ESX core resource.

### Target, phone, and keys

```lua
Config.Target = "ox_target" -- or "qb-target"
Config.Phone = "qb"
Config.VehicleKeysEvent = "vehiclekeys:client:SetOwner"
```

Supported phone configuration values include:

- `qb` for qb-phone and the shared QB/Renewed notification path
- `renewed` for Renewed Phone
- `quasar` for Quasar Smartphone
- `lb` for LB Phone
- `yseries` for YSeries

Set the vehicle-key event to the client event provided by your keys resource.

### Flatbed and winch behavior

```lua
Config.TowVehicleModel = "flatbed3"
Config.AutomaticallHookVehicle = true
Config.SetVehiclesLocked = true
Config.WarpPlayerToVehicle = false
Config.MaxCableDistance = 15.0
Config.MaxDepotDistance = 150.0
```

Keep `Config.TowVehicleModel` set to `flatbed3` unless you have intentionally rebuilt all matching flatbed behavior and assets.

### Economy and progression

```lua
Config.TowTruckDeposit = 1000
Config.FlatbedRefundAmount = 900
Config.EarnableRepMin = 50
Config.EarnableRepMax = 75
```

`Config.ContractPricing` controls distance-based contract payments and minimum payout. `Config.TowProgression` contains all 25 level thresholds, multipliers, titles, bonuses, and rewards.

### Locations and mission vehicles

The configuration also controls:

- Map blip and tow-company NPC location
- Flatbed spawn points
- Vehicle drop-off and depot coordinates
- Random contract vehicle spawn points
- Vehicle models eligible for generated contracts
- Player-facing labels and notifications

After changing coordinates, verify that each spawn and drop-off zone is clear of map props and other scripted entities.

## Commands and controls

- `/toggletow` raises or lowers the bed while using the configured flatbed.
- `/towhook` grabs or returns the hook and manages vehicle attachment.
- Use the `towremote` item to open the remote-control interface.
- The configured interaction key is shown in the in-game prompts when the player is close enough to the hook or delivery point.

## Typical job flow

1. Visit the tow-company NPC and open the towing menu.
2. Select a contract and borrow the flatbed.
3. Drive to the marked disabled vehicle.
4. Lower the bed, collect the hook, and attach it to the target vehicle.
5. Use the winch to load the vehicle, return the hook, and raise the bed.
6. Drive to the marked depot.
7. Lower the bed and unload/detach the vehicle.
8. Return to the tow-company NPC to finish the contract and receive payment and XP.

## Troubleshooting

### The resource does not start

- Confirm the folder is named exactly `reddev_towing`.
- Start `ox_lib`, `oxmysql`, `interact-sound`, and the selected framework first.
- Confirm every merged `data/` and `stream/` file is still present.
- Do not install the old tow-job or flatbed resources alongside this resource.

### The flatbed or bed object is missing

- Confirm `flatbed3` exists in the resource's `stream/` and `data/` files.
- Confirm `inm_flatbed_base.ydr` and `def_flatbed3_props.ytyp` are present.
- Confirm the manifest still contains the `DLC_ITYP_REQUEST` declaration.
- Clear the FiveM client cache after replacing streamed assets.

### The remote does not open

- Confirm the item ID is exactly `towremote`.
- Confirm the item is marked usable by the framework or inventory.
- Check that `towremote.png` is in the active inventory image directory.
- Restart the framework/inventory after adding the item definition.

### Bed or winch sounds are missing

- Confirm both OGG files were copied into the active `interact-sound` sounds directory.
- Restart `interact-sound` after installing the files.
- Check the client console and server console for missing sound-name messages.

### XP or statistics do not save

- Import `player_tow_data.sql` into the active database.
- Verify `oxmysql` is connected and started before the towing resource.
- Check that the framework returns a valid citizen/character identifier.

### Mission emails do not arrive

- Verify `Config.Phone` matches the active phone integration.
- Start the phone resource before `reddev_towing`.
- Check the configured phone resource's client event/API compatibility.

### Streaming-memory warning

FiveM may report that `flatbed3.ytd` uses substantial physical streaming memory. This originates from the supplied vehicle texture dictionary. The resource can still start, but server owners should monitor client streaming performance and optimize the textures carefully before replacing the bundled YTD.

## Validation checklist

After installation, verify all of the following in game:

- The tow-company NPC, target interaction, and contract menu appear.
- `flatbed3` spawns and the configured key resource grants ownership.
- `inm_flatbed_base` appears and moves with the flatbed.
- The bed raises and lowers without duplicate movement.
- Hook, rope, winch, attachment, detachment, and sounds work.
- The `towremote` item opens the correct UI and shows the correct image.
- A full contract awards payment and XP.
- `player_tow_data` updates after completing a job.
- Phone mission notifications arrive.
- Canceling or returning the truck cleans up spawned entities.

## Version

Current documented release: `1.0.0`.
