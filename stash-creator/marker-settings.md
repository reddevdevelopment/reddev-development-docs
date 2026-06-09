# Marker Settings

## Marker Settings

### Overview

REDDEV Stash Creator supports customizable marker settings for stash locations.

***

### Features

* Marker size customization
* Marker color customization
* Marker visibility
* Marker movement
* 3D placement
* Floating text
* Custom interaction text

***

### Example Configuration

```lua
marker = {
    enabled = true,
    type = 2,
    scale = vec3(0.3, 0.3, 0.3),
    color = {r = 255, g = 0, b = 0, a = 150},
    bobUpAndDown = false,
    rotate = true
}
```

***

### Notes

Markers can be configured differently for each stash.
