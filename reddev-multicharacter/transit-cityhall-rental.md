# Transit, City Hall, And Rentals

## Public Transit

The transit system supports configurable stops, prices, bus props/vehicles, boarding cutscenes, offboarding cutscenes, and cooldowns.

Default destination types:

* Airport.
* Bus Station.
* Car Rental Location.
* City Hall.
* Downtown.
* Hospital.
* Legion.

Each stop can have:

* Interaction coords.
* Bus spawn coords.
* Player boarding coords.
* Destination exit coords.
* Heading.
* Price.
* Description.
* Blip.

## City Hall

City Hall is the government hub.

Default functions:

* Obtain Identification.
* Employment Information.
* Beginner City Information.
* Government Services.
* Future Licensing placeholder.

Menus are config-driven so future services can be added without rewriting the system.

## Car Rental

The rental system is built to reduce pressure for every new player to immediately own a vehicle.

Configurable options include:

* Rental vehicles.
* Vehicle labels.
* Prices.
* Deposits.
* Descriptions.
* Vehicle images.
* Spawn points.
* Return points.
* Fuel provider.
* Keys provider.
* Blips and peds.

Vehicle PNGs can be added to:

```text
html/assets/vehicles
```

Then reference the image name from `config.lua`.
