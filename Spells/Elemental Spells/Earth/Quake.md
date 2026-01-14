| Spell ID     | Targeting                 | Learnable | Power | AP  | Element | Icon/Type |
| ------------ | ------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x0c`<br>12 | All<br>Always enemy party | No        | 60    | 12  | Earth   | Earth<br> |
Quake is a level 3 earth spell. It deals earth damage to everyone in the enemy party.
* As a standalone spell, its attack data can be found at
	* `BIN/BMAGIC/MAGIC012.EMI: 0000f78c` in the files
	* `0x801e878c` in the RAM
	* Normally this is 100
* The damage percentage of the first sequela can be found at
	* `BIN/BMAGIC/MAGIC012.EMI: 0000f790` in the files
	* `0x801e8790` in the RAM
	* Normally this is 25
* The damage percentage of the second sequela can be found at
	* `BIN/BMAGIC/MAGIC012.EMI: 0000f794` in the files
	* `0x801e8794` in the RAM
	* Normally this is 25