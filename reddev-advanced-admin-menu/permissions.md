# Permissions

## Permissions

### ACE Permissions

Recommended setup:

```cfg
add_ace group.admin reddev.admin allow
add_principal identifier.license:YOUR_LICENSE_HERE group.admin
```

***

### Supported Permission Systems

* ACE Permissions
* QBCore Permissions
* QBox Permissions
* ESX Groups

***

### Permission Levels

| Group | Access                   |
| ----- | ------------------------ |
| mod   | Basic moderation         |
| admin | Full admin access        |
| god   | Developer / owner access |

***

### Notes

ACE permissions are recommended for maximum compatibility and security.
