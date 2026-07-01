# Framework Compatibility

`reddev_multicharacter` includes a bridge layer for framework-specific behavior.

## Supported Frameworks

* QBCore
* Qbox / QBX
* ESX groundwork through bridge-friendly structure

QBCore and Qbox are the primary supported modes for current multicharacter behavior.

## Auto Detection

The bridge checks for common framework resources and uses the available API.

Supported Qbox resource names include:

* `qbx_core`
* `qbox`
* `qbox-core`

Supported QBCore resource names include:

* `qb-core`

## Qbox Notes

For Qbox servers, make sure the config supports external character flow where needed:

```lua
Config.Characters.UseExternalCharacters = true
```

The bridge handles:

* Player lookup.
* Citizen ID lookup.
* Money add/remove.
* Character login.
* Character delete.
* Command refresh.
* Callback fallback.
* Vehicle key entity conversion when using `qbx_vehiclekeys`.

## Inventory

Inventory support is configurable for:

* `ox_inventory`
* `qb-inventory`

Usable document items are registered server side and validated before the UI opens.

## Vehicle Keys And Fuel

Vehicle keys and fuel are routed through config and bridge helpers where available.

Recommended providers:

* `qbx_vehiclekeys`
* `qb-vehiclekeys`
* `LegacyFuel`
* `ox_fuel`

Configure the provider names in `config.lua`.
