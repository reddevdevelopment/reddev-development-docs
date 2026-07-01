# Installation

## 1. Add The Resource

Place the resource folder here:

```text
resources/[Reddev-Scripts]/reddev_multicharacter
```

Add this to `server.cfg` after framework, inventory, appearance, target, and dependency resources:

```cfg
ensure reddev_multicharacter
```

## 2. Import SQL

Import the SQL file from:

```text
sql/reddev_multicharacter.sql
```

This table tracks starter claims and prevents duplicate rewards.

## 3. Inventory Items

Add the item definitions from the resource docs/examples to your inventory system:

* QBCore: `qb-core/shared/items.lua`
* ox_inventory: `ox_inventory/data/items.lua`

Required items include:

* `bus_pass`
* `hotel_info_pamphlet`
* `vehicle_rental_pamphlet`
* `extended_stay_pamphlet`
* `temporary_id_paperwork`
* `real_estate_pamphlet`
* `employment_info_pamphlet`
* starter luggage/package items configured in `config.lua`

## 4. Configure Dependencies

Open `config.lua` and set:

* Framework mode or auto-detect.
* Inventory mode.
* Target mode.
* Vehicle keys provider.
* Fuel provider.
* Logging webhook.
* Spawn, camera, bus, transit, City Hall, and rental locations.

## 5. Restart

Restart the affected resources:

```cfg
restart reddev_multicharacter
```

Restart inventory and framework resources only if item definitions or core framework files changed.
