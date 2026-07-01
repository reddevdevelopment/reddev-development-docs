# Configuration

Most behavior is controlled from:

```text
config.lua
```

The goal is to keep server owners out of source files whenever possible.

## Main Areas

* Framework detection and bridge behavior.
* Inventory selection and usable item support.
* Target selection: `ox_target`, `qb-target`, or 3D text.
* Character preview scene, camera, ped, animation, time, and weather.
* Traveler and Citizen arrival paths.
* Starter package contents and money amounts.
* Claim mode: per account or per character.
* Transit locations, prices, headings, cooldowns, and free ride rules.
* Bus cutscene boarding/offboarding settings.
* City Hall menu options and interaction points.
* Car rental vehicles, prices, images, spawn points, fuel, and keys.
* Discord/server logging webhook.
* Document/pamphlet content.

## Recommended Editing Pattern

Change config values first, restart the resource, then test in-game with a fresh character.

Avoid editing client or server source files for normal location, reward, item, or menu changes.
