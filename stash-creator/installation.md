# Installation

## Installation

### Requirements

Before installation make sure your server has:

* ox\_lib
* oxmysql
* Supported framework
* Supported inventory system

***

### Installation Steps

1. Download the resource
2. Place the folder into your resources directory
3. Add the resource to your server.cfg
4. Configure the settings
5. Restart your server

***

### server.cfg Example

```cfg
ensure ox_lib
ensure oxmysql
ensure reddev-stashcreator
```

***

### Recommended

Always use updated dependencies and latest server artifacts.
