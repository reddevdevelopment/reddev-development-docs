# Logs

## Logs

### Logging Features

The REDDEV Advanced Admin Menu includes logging support for staff actions and moderation tracking.

***

### Supported Logs

* Player revives
* Heals
* Kicks
* Bans
* Warnings
* Vehicle spawns
* Vehicle deletions
* Spectating
* Teleports
* Inventory actions
* Screenshot actions

***

### Discord Logging

The admin menu supports Discord webhook logging.

Example:

```lua
Config.Webhooks = {
    staffActions = 'YOUR_WEBHOOK',
    moderation = 'YOUR_WEBHOOK',
    vehicles = 'YOUR_WEBHOOK'
}
```

***

### Notes

It is recommended to use separate webhooks for different log categories for better organization.
