# Testing Checklist

Do not mark the resource complete until these checks pass in-game.

## Startup

* Resource starts cleanly.
* No server console errors.
* No txAdmin console errors.
* No F8 console errors.

## Character Flow

* Character select opens.
* Existing character preview works.
* Character creation opens appearance correctly.
* Cursor and input focus work.
* Camera view is correct during appearance.
* Delete confirmation uses custom UI, not browser confirm.
* Character loading works.

## Arrival

* Traveler path works.
* Citizen path works.
* Plane arrival cutscene plays.
* RedDev Development message/logo appears during arrival.
* Custom music plays if configured.
* Player lands at the selected path.
* Player can move after the cutscene ends.

## Starter Claims

* Correct money is granted.
* Correct items are granted.
* Claim is logged to database.
* Discord/server log is created.
* Reconnect does not duplicate rewards.
* Relog does not duplicate rewards.
* Duplicate claim is blocked.

## Documents

Use every required document item and confirm the correct UI opens:

* `bus_pass`
* `hotel_info_pamphlet`
* `vehicle_rental_pamphlet`
* `extended_stay_pamphlet`
* `temporary_id_paperwork`
* `real_estate_pamphlet`
* `employment_info_pamphlet`

## Transit

* All stops show correctly.
* Prices and free ride rules work.
* Bus spawns on the ground.
* Boarding cutscene works.
* Offboarding cutscene works.
* Cooldown blocks spam.
* Blips are visible if enabled.

## City Hall

* City Hall ped/interaction works.
* Identification menu opens.
* Employment info opens.
* Beginner info opens.
* Government services opens.
* Licensing placeholder displays.

## Car Rental

* Rental UI opens.
* Vehicle images load.
* Configured vehicles display.
* Rental price is charged.
* Vehicle spawns correctly.
* Fuel is applied.
* Keys are granted.
* Return flow works if enabled.
