# FAQ

## Which resource should I install first?

Install `reddev_devtablet` first. Then add optional resources such as Music, Drug Creator, Garage Creator, Door Creator, and House Creator.

## Which resources need SQL?

SQL setup was found for `reddev_devtablet`, `doors_creator`, `drug_creator`, `garage_creator`, `reddev_housecreator`, and optional `reddev_music` tables.

## Which resources need inventory items?

Item setup was found for `reddev_devtablet`, `reddev_music`, `drug_creator`, `ammo_boxes`, `reddev-bodybag`, and `reddev_housecreator`.

## Which resources are tablet apps?

Tablet integration was found for `reddev_devtablet`, `doors_creator`, `drug_creator`, `garage_creator`, `reddev_housecreator`, and `reddev_music`.

## Can optional tablet apps be missing?

Yes. The tablet plugin docs state optional app icons hide when the app resource is stopped or missing.

## Do I need screenshots before publishing?

Fresh screenshots are recommended for the public GitBook/Tebex experience. The existing tablet screenshot guide recommends captures for Home Screen, Admin Menu, Creator Apps, Optional Apps, Runtime Menus, Drug Creator, Garage Creator, Weather and Time, and REDDEV Music.

## What should I not rename?

Do not rename streamed House Creator props files, model identifiers, or resource folders that tablet app registration depends on. Keep app IDs like `garage_creator`, `drug_creator`, and `door_creator` stable.
