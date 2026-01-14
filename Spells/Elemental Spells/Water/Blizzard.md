| Spell ID    | Targeting                 | Learnable | Power | AP  | Element | Icon/Type |
| ----------- | ------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x09`<br>9 | All<br>Always enemy party | No        | 60    | 12  | Water   | Water<br> |
Blizzard is a level 3 water spell. It deals water damage to everyone in the enemy party.
* As a standalone spell, its attack data can be found at
	* `BIN/BMAGIC/MAGIC009.EMI: 00018828` in the files
	* `0x801e9828` in the RAM
	* Normally this is 100
* The damage percentage of the first sequela can be found at
	* `BIN/BMAGIC/MAGIC009.EMI: 0001882c` in the files
	* `0x801e982c` in the RAM
	* Normally this is 25
* The damage percentage of the second sequela can be found at
	* `BIN/BMAGIC/MAGIC009.EMI: 00018830` in the files
	* `0x801e9830` in the RAM
	* Normally this is 25