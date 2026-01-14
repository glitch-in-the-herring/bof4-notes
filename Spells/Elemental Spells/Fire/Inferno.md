
| Spell ID    | Targeting                  | Learnable | Power | AP  | Element | Icon/Type |
| ----------- | -------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x03`<br>3 | Single<br>Enemy party only | No        | 80    | 10  | Fire    | Fire<br>  |
Inferno is a level 3 fire spell. It deals fire damage to a single target.
* As a standalone spell, its attack data can be found at
	* `BIN/BMAGIC/MAGIC003.EMI: 00017e60` in the files
	* `0x801e8e60` in the RAM
	* Normally this is 100
* The damage percentage of the first sequela can be found at
	* `BIN/BMAGIC/MAGIC003.EMI: 00017e64` in the files
	* `0x801e8e64` in the RAM
	* Normally this is 25
* The damage percentage of the second sequela can be found at
	* `BIN/BMAGIC/MAGIC003.EMI: 00017e68` in the files
	* `0x0x801e8e68` in the RAM
	* Normally this is 25