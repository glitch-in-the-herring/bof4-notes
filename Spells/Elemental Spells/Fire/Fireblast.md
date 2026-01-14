
| Spell ID    | Targeting                 | Learnable | Power | AP  | Element | Icon/Type |
| ----------- | ------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x02`<br>2 | All<br>Always enemy party | No        | 30    | 6   | Fire    | Fire<br>  |
Fireblast is a level 2 fire spell. It deals fire damage to everyone in the enemy party.
* As a standalone spell, its attack data can be found at
	* `BIN/BMAGIC/MAGIC002.EMI: 00017e38` in the files
	* `0x801e8e38` in the RAM
	* Normally this is 100
* The damage percentage of the first sequela can be found at
	* `BIN/BMAGIC/MAGIC002.EMI: 00017e3c` in the files
	* `0x801e8e3c` in the RAM
	* Normally this is 25
* The damage percentage of the second sequela can be found at
	* `BIN/BMAGIC/MAGIC002.EMI: 00017e40` in the files
	* `0x801e8e40` in the RAM
	* Normally this is 25