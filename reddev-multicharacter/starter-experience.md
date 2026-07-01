# Starter Experience

New characters can choose one arrival path.

The selected path controls:

* Arrival scene.
* Spawn location.
* Starting money.
* Starter package contents.
* Documents and pamphlets received.
* Claim logging metadata.

## Traveler

Traveler is for a new person arriving with limited resources and looking for opportunity.

Default rewards:

* $2,500 cash.
* $5,000 bank.
* Basic cell phone.
* Bus pass.
* Hotel information pamphlet.
* Vehicle rental pamphlet.
* Extended stay motel and hotel information.

Default arrival:

```text
Bus Station
```

## Citizen

Citizen is for someone officially relocating and starting a new life.

Default rewards:

* $5,000 cash.
* $10,000 bank.
* Brand new cell phone.
* Temporary identification paperwork.
* Real estate information pamphlet.
* Employment information pamphlet.

Default arrival:

```text
Airport
```

## Claim Protection

Starter rewards can only be claimed once based on config.

Supported claim modes:

* Per account.
* Per character.

The SQL table records:

* Citizen ID.
* License.
* Selected path.
* Claimed state.
* Claim timestamp.
* Metadata JSON.

Every claim should be logged to Discord/server logs with player name, identifiers, rewards, and timestamp.
