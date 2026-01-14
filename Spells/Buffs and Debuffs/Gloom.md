| Spell ID      | Targeting                                       | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | ----------------------------------------------- | --------- | ----- | --- | ------- | --------- |
| `0xc4`<br>196 | Single<br>Enemy or player party (front or back) | No        | 0<br> | 0   | Status  | Normal    |
Gloom sets the holy resistance of its target to 2. Not low enough to cause any damage because of healing, but low enough that Kyrie will kill the target. Its sequela is more holy resistance reduction.
The replacement resistance value can be found at 
* `BIN/SYSTEM/GAME.EMI: 00009af4` in the game's files
* `0x80196af4` in the RAM

* As a standalone spell, the stat change data can be found at:
	* `BIN/BMAGIC/MAGIC196.EMI: 0001249c` in the files
	* `0x801e749c`in the RAM 
	* Normally targets the holy resistance
* The first sequela's stat change data can be found at:
	* `BIN/BMAGIC/MAGIC196.EMI: 000124a0` in the files
	* `0x801e74a0`in the RAM 
	* Normally targets the holy resistance
* The second sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC196.EMI: 000124a4` in the files
	* `0x801e74a4`in the RAM 
	* Normally targets the holy resistance
* The third sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC196.EMI: 000124a8` in the files
	* `0x801e74a8`in the RAM 
	* Normally targets the holy resistance

