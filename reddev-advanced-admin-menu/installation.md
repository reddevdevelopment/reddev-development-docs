# Installation

## Installation

### Version

#### 0.1.56 BETA

***

## Overview

REDDEV Advanced Admin Menu now includes a fully redesigned tablet-style admin experience while keeping the standard `/admin` menu and F10 support available.

The new tablet system introduces app-style navigation, dashboard widgets, tablet shell styling, and optional inventory item support.

***

## Requirements

Before installation make sure your server has:

* ox\_lib
* oxmysql
* screenshot-basic (optional)
* Supported framework installed correctly

***

## Supported Frameworks

* QBCore
* QBox
* ESX

***

## Installation Steps

1. Download the latest version from Tebex
2. Place the resource inside your resources folder
3. Add the resource to your `server.cfg`
4. Configure permissions
5. Configure tablet item support if desired
6. Restart your server

***

## server.cfg Example

```cfg
ensure ox_lib
ensure oxmysql
ensure reddev-admin
```

***

## Tablet System

### Added Features

* Added `/admintablet` as a tablet-first launcher
* Added `Config.TabletItem` support for inventory items
* Added tablet home screen with app-style admin navigation
* Added rounded tablet shell styling
* Added dashboard widgets
* Added Home button navigation inside tablet apps

***

## Tablet Applications

The tablet interface includes:

* Dashboard
* Players
* Characters
* Vehicles
* Garages
* Map
* Items
* Jobs / Gangs
* Reports
* Logs
* Duty
* Weather
* Commands
* Addons
* Settings
* Themes

***

## Tablet Item Configuration

### Example Config

```lua
Config.TabletItem = 'admin_tablet'
```

***

### Example QBCore Item

```lua
['admintablet'] = {
    name = 'admin_tablet',
    label = 'Admin Tablet',
    weight = 500,
    type = 'item',
    image = 'admin_tablet.png',
    unique = true,
    useable = true,
    shouldClose = true,
    combinable = nil,
    description = 'Advanced REDDEV administration tablet'
},
```

***

## Commands

| Command        | Description                   |
| -------------- | ----------------------------- |
| `/admin`       | Opens the standard admin menu |
| `/admintablet` | Opens the tablet interface    |

***

## Notes

* Existing admin systems remain fully functional
* F10 support is still available
* Tablet apps use the existing wired admin panels internally
* Compatible with QBCore, QBox, and ESX
* Recommended to use latest server artifacts
