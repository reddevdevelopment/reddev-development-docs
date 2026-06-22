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

## REDDEV Shops Restart Freezes

- Tune startup batching in `reddev-shops/config.lua`:

```lua
Config.Performance.spawnBatchSize = 1
Config.Performance.spawnBatchDelay = 200
Config.Performance.lazyPedSpawning = true
Config.Performance.lazyPedSpawnPerScan = 1
```

- Tune riddle startup in `reddev-shops/modules/riddles/config.lua`:

```lua
RiddleConfig.Performance.spawnBatchDelay = 250
RiddleConfig.Performance.lazyPedSpawning = true
RiddleConfig.Performance.lazyPedSpawnPerScan = 1
RiddleConfig.Performance.lazyPedScanWait = 1500
```

- Make sure old separate shop, riddle, delivery, or `qb-shops` resources are stopped.

## REDDEV Shops Purchases Say Not Enough Money

- Confirm the shop payment method is correct.
- If cash is stored as an inventory item, keep `Config.CashItemName = "cash"` and `Config.AllowCashMoneyFallback = true`.
- Riddle entry fees also support cash-as-item and optional bank fallback through `RiddleConfig.AllowBankFallback`.

## REDDEV Shops XP Still Blocks Purchases

- If shops should not use XP, set this in `reddev-shops/config.lua`:

```lua
Config.UseXpSystem = false
```

- Restart `reddev-shops` after changing it.
- When disabled, the menu hides XP requirements and the server ignores item `xpNeeded` checks.

## REDDEV Shops /xp Display Missing

- Confirm `Config.XpDisplay.enabled = true`.
- Confirm the command name in `Config.XpDisplay.command`.
- Keep `Config.XpDisplay.useNui = true` for the small REDDEV NUI card.
- Set `Config.XpDisplay.persistent = true` if the XP display should stay on screen.

## Riddle Peds Moved Or Arrival Message Appears

This is controlled by `reddev-shops/modules/riddles/config.lua`:

```lua
RiddleConfig.RandomSpawns.enabled = true
RiddleConfig.RandomSpawns.moveEveryMinutes = 20
RiddleConfig.RandomSpawns.arrivalWatermark.text = "Riddles Have Arrived!"
RiddleConfig.RandomSpawns.arrivalWatermark.durationSeconds = 20
```

Set `RiddleConfig.RandomSpawns.enabled = false` to keep riddle peds at static coordinates.

## Players Stuck In Tablet Or Housing UI

- Use `/reddevunstuck`, `/rdunstuck`, or `/reddevreset`.
- For House Creator, use `/reddevhouseunstuck` or `/houseunstuck`.
- Keep automatic cleanup enabled in `reddev_devtablet/config.lua`.

## House Props Missing

- Start `reddev_housecreator_props` before `reddev_housecreator`.
- Do not rename or remove stream files.
- Restart both resources after changing start order.
