# Usable Documents

Starter document items are functional inventory items.

Using a document opens a custom RedDev Development document UI with configurable page content.

## Required Items

* `bus_pass`
* `hotel_info_pamphlet`
* `vehicle_rental_pamphlet`
* `extended_stay_pamphlet`
* `temporary_id_paperwork`
* `real_estate_pamphlet`
* `employment_info_pamphlet`

## Behavior

* Server validates that the player owns the item.
* Invalid or missing items are rejected.
* UI content is loaded from config.
* ESC and close button both close the document.
* The same UI supports paper, brochure, pamphlet, pass, and paperwork layouts.

## Editing Content

Edit document content in:

```lua
Config.Documents = {
    hotel_info_pamphlet = {
        label = "Hotel Information Pamphlet",
        title = "Extended Stay & Hotel Information",
        subtitle = "Welcome to RedDev Development",
        documentType = "brochure",
        pages = {
            {
                heading = "Temporary Housing",
                body = "Use this section to explain hotel or motel options."
            }
        }
    }
}
```

Do not hardcode production document text inside NUI JavaScript.
