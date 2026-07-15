---
cover: http://127.0.0.1:39451/reddevmulticharater.png
coverY: 0
---

# REDDEV Multicharacter

### Overview

REDDEV Multicharacter v1.0.0 provides a cinematic character-selection and first-arrival flow for QBCore and Qbox servers. It combines character slots, Traveler and Citizen starting paths, starter packages, transit, City Hall services, rentals, and usable arrival documents in one resource.



### Features

* Built-in character slot, create, load, delete, and disconnect flow.
* Up to five character slots by default.
* Traveler and Citizen starting paths with configurable spawn points, money, items, and package behavior.
* Cinematic character preview, intro sequence, and bus transit cutscenes.
* Database-backed starter-claim validation with per-character or per-account modes.
* Package or direct-grant starter reward modes.
* Configurable public transit with fares, new-player free rides, cooldowns, targets, and text fallback.
* City Hall services, car rentals, vehicle keys, fuel, garage detection, and map blips.
* Usable starter luggage, transit pass, and informational documents.
* NUI, qb-menu, or ox\_lib menu selection.

### Requirements

Required:



* qb-core or qbx\_core for the verified built-in character selector.
* oxmysql.
* FiveM spawnmanager.

Optional, based on configuration:



* illenium-appearance for the verified appearance editor and saved preview appearance.
* qb-inventory or ox\_inventory.
* qb-target or ox\_target; text interaction is the fallback.
* qb-menu or ox\_lib when not using the included NUI menu.
* A supported vehicle keys, fuel, or garage resource when those integrations are enabled.

### Installation

1. Place the reddev\_multicharacter folder in your FiveM resources directory.
2. Import sql/reddev\_multicharacter.sql.
3. Copy only the required item entries into your active inventory. Do not replace your entire items file.
4. Copy the included item images to the matching image folder for your inventory, preserving filenames and capitalization.
5. If the built-in selector is enabled, disable qb-multicharacter so both selectors do not start together.
6. On Qbox, set config.characters.useExternalCharacters = true in qbx\_core.
7. Configure config.lua.
8. Start the resource after the framework, oxmysql, inventory, appearance, target, menu, keys, fuel, and garage resources it uses.
9. Restart reddev\_multicharacter and test with a fresh character slot.

### Configuration

Important defaults in config.lua:



* Config.Framework = 'auto': detects Qbox, QBCore, then ESX bridge services; the verified built-in selector is QBCore/Qbox.
* Config.Inventory = 'auto': detects ox\_inventory, then qb-inventory, then framework fallback.
* Config.Target = 'auto': detects ox\_target, then qb-target, then text interaction.
* Config.Menu = 'nui': supported values are nui, qb-menu, and ox\_lib.
* Config.ClaimMode = 'per\_character': use per\_account for one starter claim per Rockstar license.
* Config.Multicharacter.MaxCharacters = 5.
* Config.Package.Mode = 'package': use direct to grant configured rewards without a package item.
* Config.Arrival, Config.Transit, Config.CityHall, and Config.CarRental control their respective flows.

Restart the resource after changing configuration. Do not publish webhook values or other private server settings.



### Character Flow

Character slots → Create character → Choose Traveler or Citizen → Complete appearance → Play the configured intro → Spawn at the selected arrival point → Receive the validated package or direct rewards.



Existing characters can be selected from the same cinematic slot interface. Character deletion is controlled by Config.Multicharacter.EnableDeleteButton.



### Framework Support

QBCore and Qbox are the verified frameworks for the built-in character selector, login, logout, deletion, rewards, documents, transit, City Hall, and rental flow. Qbox uses qbx\_core and requires external character handling to be enabled.



The config contains ESX bridge detection for supporting services, but this release does not advertise the built-in multicharacter selector as verified for ESX.



### Appearance Support

illenium-appearance is the verified appearance integration. It provides the creation editor, saves the new appearance, and restores saved appearance data for character previews. If it is not running, the resource warns the player and continues the arrival flow without opening that editor.



### Items

The default configuration references:



* duffle\_bag
* suitcase
* starter\_backpack
* welcome\_package
* phone
* bus\_pass
* hotel\_info\_pamphlet
* vehicle\_rental\_pamphlet
* extended\_stay\_pamphlet
* temporary\_id\_paperwork
* real\_estate\_pamphlet
* employment\_info\_pamphlet
* city\_information\_pamphlet

Use only the item definition file for your active inventory. Package and document images are included in the release; preserve their exact filenames. The phone item must match the phone resource installed on your server.



### Commands

The release does not register a player command for its main workflow. Character selection uses the NUI, while transit, City Hall, rentals, packages, and documents use configured items, targets, menus, or text interactions.



### Exports

No general-purpose public developer exports are documented for this release. ox\_inventory item definitions use the packaged server exports in the form reddev\_multicharacter.\<item\_name> for the included luggage, package, pass, and document items. Copy the supplied definitions exactly instead of inventing export names.



### Troubleshooting

* Resource reports a missing script: confirm config.lua is present beside fxmanifest.lua and start the completed release folder.
* Two character selectors appear: stop qb-multicharacter when the REDDEV selector replaces it.
* Qbox opens its default selector: set config.characters.useExternalCharacters = true.
* Appearance editor does not open: ensure illenium-appearance starts before reddev\_multicharacter.
* Starter package or document is missing: verify the exact item ID exists in the active inventory and its image was copied.
* Claims do not save: import sql/reddev\_multicharacter.sql, confirm oxmysql is running, and verify the database table exists.
* Targets or menus do not appear: confirm Config.Target and Config.Menu match a running resource, or use the text/NUI fallback.
* Rental keys, fuel, or garage state fail: verify the selected integration is installed, started first, and configured under the matching bridge option.

### Support

For installation help, include the resource version, framework, inventory, target, relevant configuration selections, and complete server/F8 error text. Never send license keys, database credentials, or webhook URLs.





