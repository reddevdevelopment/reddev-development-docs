# Screenshot System

## Screenshot System

### Overview

The REDDEV Advanced Admin Menu includes screenshot functionality for staff monitoring and evidence collection.

***

### Supported Systems

* screenshot-basic
* FiveManage

***

### Features

* Capture player screenshots
* Save screenshots automatically
* Discord logging support
* Staff monitoring integration

***

### screenshot-basic Setup

Add to your server.cfg:

```cfg
ensure screenshot-basic
```

***

### Example

```lua
exports['screenshot-basic']:requestClientScreenshot(playerId, {
    fileName = 'screenshots/player.jpg'
})
```

***

### Notes

Some hosting providers may require filesystem permissions for screenshot saving.
