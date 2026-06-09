# Common Errors

## Tablet App Icon Missing

- Confirm the optional resource is started.
- Restart `reddev_devtablet` after starting optional apps.
- Confirm the optional resource has a tablet app event or app JSON, such as `doors_creator:openTablet`, `drug_creator:openTablet`, or `garage_creator:openTablet`.

## SQL Errors

- Start `oxmysql` before SQL-backed REDDEV resources.
- Run the SQL files manually if your database user cannot create tables automatically.
- Use the correct framework SQL file. QBCore/Qbox uses QB SQL; ESX uses ESX SQL.
- For House Creator, follow `[sql]/README_RUN_ORDER.md` exactly.

## No Permission

- Add REDDEV tablet ACE permissions:

```cfg
add_ace group.admin reddev_admin.open allow
add_ace group.admin reddev_admin.admin allow
```

- Add Door Creator ACE permissions:

```cfg
add_ace group.admin doors_creator allow
add_ace group.admin reddev_door_creator allow
```

- Check resource config for job, gang, grade, identifier, and admin group lists.

## Items Do Not Work

- Confirm item names match exactly.
- Add items to the correct framework or inventory item file.
- Copy PNG images to the active inventory image folder.
- Restart the framework/inventory resource after editing items.

## Target Options Missing

- Confirm target mode is enabled in the resource config.
- Confirm the selected target resource is started.
- If using floating text, confirm the resource has target disabled and prompt distances are reasonable.

## Players Stuck In Tablet Or Housing UI

- Use `/reddevunstuck`, `/rdunstuck`, or `/reddevreset`.
- For House Creator, use `/reddevhouseunstuck` or `/houseunstuck`.
- Keep automatic cleanup enabled in `reddev_devtablet/config.lua`.

## House Props Missing

- Start `reddev_housecreator_props` before `reddev_housecreator`.
- Do not rename or remove stream files.
- Restart both resources after changing start order.
