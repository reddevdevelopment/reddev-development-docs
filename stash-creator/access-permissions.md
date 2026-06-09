# Access Permissions

## Access Permissions

### Overview

Stashes can be restricted using jobs, gangs, identifiers, or admin permissions.

***

### Supported Restrictions

* Job locked stashes
* Gang locked stashes
* Admin only stashes
* Public stashes
* Identifier locked stashes

***

### Example

```lua
stash.access = {
    jobs = {
        police = 0,
        ambulance = 0
    }
}
```

***

### Notes

Access permissions can be configured individually for each stash.
