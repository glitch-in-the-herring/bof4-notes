| Spell ID     | Secondary resistance | Targeting                  | Learnable | Power | AP  | Element | Icon/Type |
| ------------ | -------------------- | -------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x1e`<br>30 | Magic                | Single<br>Enemy party only | No        | 0     | 13  | Death   | Death     |
Death is a spell that instantly kills a target, if successful. Its attack data can be found at:
* `BIN/BMAGIC/MAGIC030.EMI: 00017bf8` in the game's files
* `0x801e8bf8` in the RAM
* Normally this causes instant death for a single target.
Death uses the [[General Success Rate Formula]]. Its primary resistance is death, and its secondary resistance is magic.