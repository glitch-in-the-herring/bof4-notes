| Spell ID    | Targeting                  | Learnable | Power | AP  | Element | Icon/Type |
| ----------- | -------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x08`<br>8 | Single<br>Enemy party only | No        | 40    | 5   | Water   | Water<br> |
Ice Blast is a level 2 water spell. It deals water damage to a single target.
* As a standalone spell, its attack data can be found at
	* `BIN/BMAGIC/MAGIC008.EMI: 00015ac0` in the files
	* `0x801e8ac0` in the RAM
	* Normally this is 100
* The damage percentage of the first sequela can be found at
	* `BIN/BMAGIC/MAGIC008.EMI: 00015ac4` in the files
	* `0x801e8ac4` in the RAM
	* Normally this is 25
* The damage percentage of the second sequela can be found at
	* `BIN/BMAGIC/MAGIC008.EMI: 00015ac8` in the files
	* `0x801e8ac8` in the RAM
	* Normally this is 25