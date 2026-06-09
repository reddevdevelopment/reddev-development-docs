# REDDEV House Creator Props

## Overview

REDDEV House Creator Props is the streamed asset package required by REDDEV House Creator. It contains shells, furniture models, creator props, signs, island assets, decor assets, textures, and item placement files used by the housing system.

## Features

- Streams furniture and housing prop models.
- Loads required `.ytyp` item placement files.
- Registers extra furniture into REDDEV House Creator.
- Provides shell and creator assets used by housing interiors.
- Keeps required model, texture, and stream files available to clients.

## Dependencies

- Required by `reddev_housecreator`.
- Manifest dependency `/assetpacks`.
- Streamed asset files in the `stream/` folder.

## Installation

- Place `reddev_housecreator_props` in `resources/[Reddev-Scripts]/reddev_housecreator_props`.
- Start it before `reddev_housecreator`.
- Do not remove or rename files inside `stream/`.
- Restart both props and House Creator after changing start order.

## Server.cfg Ensure Order

```cfg
ensure reddev_housecreator_props
ensure reddev_housecreator
```

## Configuration

- No editable config file was found.
- Keep streamed file names and model identifiers stable.
- `server/register_furniture.lua` registers furniture data with House Creator.

## Commands

- No chat commands were found.

Public exports detected:

- None found in the scanned files.

Public/admin events detected:

- None documented as customer/admin entry points.

## Items

- No inventory item definitions were found in this props package.

## Permissions

- No ACE, job, gang, identifier, or group checks were found.

## Inventory Support

- No inventory integration was found.

## Framework Support

- Framework independent streamed asset package.

## Target Support

- No target integration was found.

## Database or SQL Setup

- No SQL files were found.

## Troubleshooting

- If props do not appear, confirm the resource is started and starts before `reddev_housecreator`.
- If models are missing, confirm the `stream/` folder still contains the included `.ydr`, `.ytd`, `.ytyp`, `.ymap`, `.meta`, and related files.
- If F8 shows missing model warnings, restore the original stream files and restart both resources.

## FAQ

- **Can I rename streamed files?** The README says not to rename files or model names.
- **Is this optional?** No. It is required by `reddev_housecreator`.
- **Should I also start an old grouped props folder?** No. The README says this replaces the old grouped props folder for this addon.
