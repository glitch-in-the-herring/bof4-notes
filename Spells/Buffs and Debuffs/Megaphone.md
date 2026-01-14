| Spell ID     | Targeting                 | Learnable | Power | AP  | Element | Icon/Type       |
| ------------ | ------------------------- | --------- | ----- | --- | ------- | --------------- |
| `0x5c`<br>92 | All<br>Always enemy party | Yes<br>3  | 0<br> | 4   | Status  | Melee<br>ST DWN |
Megaphone is both a buff and debuff for the enemy party: it raises the enemies' PWR while lowering their DEF. Its sequela is additional increase to the PWR and additional decrease to the DEF. 
## PWR
* As a standalone spell, PWR's stat change data can be found at:
	* `BIN/BMAGIC/MAGIC092.EMI: 000012d4` in the files
	* `0x801e72d4`in the RAM 
	* Normally this is 40
* The first sequela's stat change data can be found at:
	* `BIN/BMAGIC/MAGIC040.EMI 000012d8`in the files
	* `0x801e72d8`in the RAM
	* Normally this is 44.
* The second sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC040.EMI 000012dc in the files
	* `0x801e72dc` in the RAM
	* Normally this is 52.
* The third sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC040.EMI 000012e0` in the files
	* `0x801e72e0` in the RAM
	* Normally this is 0.
## DEF
* As a standalone spell, DEF's stat change data can be found at:
	* `BIN/BMAGIC/MAGIC092.EMI: 000012e4` in the files
	* `0x801e72e4`in the RAM 
	* Normally this is 40
* The first sequela's stat change data can be found at:
	* `BIN/BMAGIC/MAGIC040.EMI 000012e8`in the files
	* `0x801e72e8`in the RAM
	* Normally this is 44.
* The second sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC040.EMI 000012ec in the files
	* `0x801e72ec` in the RAM
	* Normally this is 52.
* The third sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC040.EMI 000012f0` in the files
	* `0x801e72f0` in the RAM
	* Normally this is 8.