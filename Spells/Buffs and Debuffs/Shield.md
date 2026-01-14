| Spell ID     | Targeting                                      | Learnable | Power        | AP  | Element | Icon/Type |
| ------------ | ---------------------------------------------- | --------- | ------------ | --- | ------- | --------- |
| `0x28`<br>40 | `0x47`<br>All<br>Enemy or player party (front) | No        | 20<br>Unused | 6   | None    | ST UP     |

The targets-all variant of Protect, it gives a 20% buff to protection for every use, up to 100%. Its [[Sequela]] is an extra increase in defense.

* As a standalone spell, the stat change data can be found at:
	* `BIN/BMAGIC/MAGIC040.EMI 0x0001332c` in the files
	* `0x801e932c`in the RAM 
	* Normally this is 20
* The first sequela's stat change data can be found at:
	* `BIN/BMAGIC/MAGIC040.EMI 0x00013330`in the files
	* `0x801e9330`in the RAM
	* Normally this is 22.
* The second sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC040.EMI 0x00013334` in the files
	* `0x801e9334` in the RAM
	* Normally this is 26.
* The third sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC040.EMI 0x00013338` in the files
	* `0x801e9338` in the RAM
	* Normally this is 4.
## Limits
See [[Limits]] for info on modifying the limits