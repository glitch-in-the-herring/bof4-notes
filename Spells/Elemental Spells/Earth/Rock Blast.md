| Spell ID     | Targeting                 | Learnable | Power | AP  | Element | Icon/Type |
| ------------ | ------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x0a`<br>10 | All<br>Always enemy party | No        | 15    | 4   | Earth   | Earth<br> |
Rock Blast is a level 1 earth spell. It deals earth damage to everyone in the enemy party.
* As a standalone spell, its attack data can be found at
	* `BIN/BMAGIC/MAGIC010.EMI: 00017f80` in the files
	* `0x801e8f80` in the RAM
	* Normally this is 100
* The damage percentage of the first sequela can be found at
	* `BIN/BMAGIC/MAGIC010.EMI: 00017f84` in the files
	* `0x801e8f84` in the RAM
	* Normally this is 25
* The damage percentage of the second sequela can be found at
	* `BIN/BMAGIC/MAGIC010.EMI: 00017f88` in the files
	* `0x801e8f88` in the RAM
	* Normally this is 25