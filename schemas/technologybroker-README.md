# EDDN TechnologyBroker Schema

## Introduction
Here we document how to take data from an ED `TechnologyBroker` Journal Event and
properly structure it for sending to EDDN.

Please consult [EDDN Schemas README](./README-EDDN-schemas.md) for general
documentation for a schema such as this.

If you find any discrepancies between what this document says and what is
defined in the relevant Schema file, then you should, in the first instance,
assume that it is the Schema file that is correct.
**PLEASE open [an issue on GitHub](https://github.com/EDCD/EDDN/issues/new/choose)
to report any such anomalies you find so that we can check and resolve the
discrepancy.**

## Senders
The primary data source for this schema is the ED Journal event `TechnologyBroker`.
This event occurs when a commander unlocks new technology at a Technology Broker.

### Required Fields
The following fields from the Journal event **MUST** be included:
- `timestamp` - When the technology was unlocked
- `event` - Always "TechnologyBroker"
- `MarketID` - The unique identifier for the station's market
- `BrokerType` - The type of technology broker (e.g. "guardian", "human", "sirius")

### Elisions
You **MUST** remove the following key/value pairs from the data:
- `ItemsUnlocked` - This is the list of items that were unlocked
- `Commodities` - This is the list of commodities that were paid for the unlock
- `Materials` - This is the list of materials that were paid for the unlock

### Rate Limiting
Since these values can occur multiple times in a short timespan, senders
*must* take care to only send them once at most while docked at a station.

### Augmentations
#### horizons and odyssey flags
Please read [horizons and odyssey flags](../docs/Developers.md#horizons-and-odyssey-flags)
in the Developers' documentation.

#### gameversion and gamebuild
You **MUST** always set these as per [the relevant section](../docs/Developers.md#gameversions-and-gamebuild)
of the Developers' documentation. 