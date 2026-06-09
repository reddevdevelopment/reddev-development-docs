# Dependencies

## Dependencies

### Required Dependencies

The REDDEV Advanced Admin Menu requires the following resources to function correctly.

***

### Core Dependencies

#### ox\_lib

Required for UI components, notifications, menus, callbacks, and utility functions.

```cfg
ensure ox_lib
```

***

#### oxmysql

Required for database communication and data storage.

```cfg
ensure oxmysql
```

***

### Optional Dependencies

#### screenshot-basic

Used for screenshot capture features.

```cfg
ensure screenshot-basic
```

***

#### FiveManage

Optional integration for advanced screenshot and media handling.

***

### Supported Frameworks

* QBCore
* QBox
* ESX

***

### Notes

Make sure all dependencies are started before the admin menu resource.
