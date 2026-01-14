
| Spell ID     | Targeting                                                 | Learnable | Power        | AP  | Element | Icon/Type |
| ------------ | --------------------------------------------------------- | --------- | ------------ | --- | ------- | --------- |
| `0x29`<br>41 | `0x4e`<br>Single<br>Enemy or player party (front or back) | No        | 50<br>Unused | 2   | None    | ST UP     |
Unlike the other primary stat buffs, Speed gives a 50% agility buff, up to 100%. Its [[Sequela]] is an extra increase in agility.
* As a standalone spell, the stat change data can be found at:
	* `BIN/BMAGIC/MAGIC038.EMI 0x00012d68` in the files
	* `0x801e8d68`in the RAM 
	* Normally this is 50 and targets speed
* The first sequela's stat change data can be found at:
	* `BIN/BMAGIC/MAGIC038.EMI 0x00012d6c`in the files
	* `0x801e8d6c`in the RAM
	* Normally this is 55 and targets speed
* The second sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC038.EMI 0x00012d70` in the files
	* `0x801e8d70` in the RAM
	* Normally this is 65 and targets speed
* The third sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC038.EMI 0x00012d74` in the files
	* `0x801e8d74` in the RAM
	* Normally this is 10 and targets speed
### Limits
See [[Limits]] for info on modifying the limits