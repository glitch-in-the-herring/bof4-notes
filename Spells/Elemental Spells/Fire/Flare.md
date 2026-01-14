
| Spell ID    | Targeting                  | Learnable | Power | AP  | Element | Icon/Type |
| ----------- | -------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x01`<br>1 | Single<br>Enemy party only | No        | 15    | 3   | Fire    | Fire<br>  |
Flare is a level 1 fire spell. It deals fire damage to a single target.
* As a standalone spell, its attack data can be found at
	* `BIN/BMAGIC/MAGIC001.EMI: 0000edbc` in the files
	* `0x801e85bc` in the RAM
	* Normally this is 100
* The damage percentage of the first sequela can be found at
	* `BIN/BMAGIC/MAGIC001.EMI: 0000edc0` in the files
	* `0x801e85c0` in the RAM
	* Normally this is 25
* The damage percentage of the second sequela can be found at
	* `BIN/BMAGIC/MAGIC001.EMI: 0000edc4` in the files
	* `0x801e85c4` in the RAM
	* Normally this is 25