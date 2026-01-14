| Spell ID      | Targeting                          | Learnable | Power       | AP  | Element | Icon/Type |
| ------------- | ---------------------------------- | --------- | ----------- | --- | ------- | --------- |
| `0x92`<br>146 | All<br>Always player party (front) | Yes<br>7  | 0<br>Unused | 20  | Stat    | ST UP     |
Unlike the other buff spells, the [[stat change data]] for War Shout is not the percentage of the target stat's increase, but a multiplier for the faerie calculations.
* As a standalone spell, the stat change data can be found at:
	* `BIN/BMAGIC/MAGIC146.EMI 0000203c` in the files
	* `0x801e803c`in the RAM 
	* Normally this is 100
* The first sequela's stat change data can be found at:
	* `BIN/BMAGIC/MAGIC146.EMI 00002040`in the files
	* `0x801e8040`in the RAM
	* Normally this is 110.
* The second sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC146.EMI 00002044` in the files
	* `0x801e8044` in the RAM
	* Normally this is 130.
* The third sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC146.EMI 00002048` in the files
	* `0x801e8048` in the RAM
	* Normally this is 20