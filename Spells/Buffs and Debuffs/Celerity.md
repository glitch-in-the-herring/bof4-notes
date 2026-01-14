
| Spell ID      | Targeting | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | --------- | --------- | ----- | --- | ------- | --------- |
| `0x6e`<br>110 | Self      | Yes<br>7  | 0<br> | 0   | None    | ST UP     |
Celerity is a buff that doubles the user's PWR, DEF, AGL, and WIS. It can only be used once every three hours. It has sequelae.
## PWR
* As a standalone spell, the PWR stat change data can be found at:
	* `BIN/BMAGIC/MAGIC110.EMI: 000129e0` in the files
	* `0x801e89e0`in the RAM 
	* Normally this is 100
* The first sequela's PWR stat change data can be found at:
	* `BIN/BMAGIC/MAGIC110.EMI: 000129e4`in the files
	* `0x8801e89e4`in the RAM
	* Normally this is 100.
* The second sequela's PWR stat change data can be found at
	* `BIN/BMAGIC/MAGIC110.EMI: 000129e8` in the files
	* `0x801e89e8` in the RAM
	* Normally this is 100.
* The third sequela's PWR stat change data can be found at
	* `BIN/BMAGIC/MAGIC110.EMI: 000129ec` in the files
	* `0x801e89ec` in the RAM
	* Normally this is 20.
## DEF
* As a standalone spell, the DEF stat change data can be found at:
	* `BIN/BMAGIC/MAGIC110.EMI: 000129f0` in the files
	* `0x801e89f0`in the RAM 
	* Normally this is 100
* The first sequela's DEF stat change data can be found at:
	* `BIN/BMAGIC/MAGIC110.EMI: 000129f4`in the files
	* `0x8801e89f4`in the RAM
	* Normally this is 100.
* The second sequela's DEF stat change data can be found at
	* `BIN/BMAGIC/MAGIC110.EMI: 000129f8` in the files
	* `0x801e89f8` in the RAM
	* Normally this is 100.
* The third sequela's DEF stat change data can be found at
	* `BIN/BMAGIC/MAGIC110.EMI: 000129fc` in the files
	* `0x801e89fc` in the RAM
	* Normally this is 20.
## AGL
* As a standalone spell, the AGL stat change data can be found at:
	* `BIN/BMAGIC/MAGIC110.EMI: 00012a00` in the files
	* `0x801e8a00`in the RAM 
	* Normally this is 100
* The first sequela's AGL stat change data can be found at:
	* `BIN/BMAGIC/MAGIC110.EMI: 00012a04`in the files
	* `0x8801e8a04`in the RAM
	* Normally this is 100.
* The second sequela's AGL stat change data can be found at
	* `BIN/BMAGIC/MAGIC110.EMI: 00012a08` in the files
	* `0x801e8a08` in the RAM
	* Normally this is 100.
* The third sequela's AGL stat change data can be found at
	* `BIN/BMAGIC/MAGIC110.EMI: 00012a0c` in the files
	* `0x801e8a0c` in the RAM
	* Normally this is 20.
## WIS
* As a standalone spell, the WIS stat change data can be found at:
	* `BIN/BMAGIC/MAGIC110.EMI: 00012a10` in the files
	* `0x801e8a10`in the RAM 
	* Normally this is 100
* The first sequela's WIS stat change data can be found at:
	* `BIN/BMAGIC/MAGIC110.EMI: 00012a14`in the files
	* `0x8801e8a14`in the RAM
	* Normally this is 100.
* The second sequela's WIS stat change data can be found at
	* `BIN/BMAGIC/MAGIC110.EMI: 00012a18` in the files
	* `0x801e8a18` in the RAM
	* Normally this is 100.
* The third sequela's WIS stat change data can be found at
	* `BIN/BMAGIC/MAGIC110.EMI: 00012a1c` in the files
	* `0x801e8a1c` in the RAM
	* Normally this is 20.
## Timer
Celerity takes three hours to cool down. This is tracked by means of a count down located at:
* `0x8011b740` in the RAM (`HH`)
* `0x8011b744` in the RAM (`MM:SS:ff`)
* `+0xf74` in the save file (`HH`)
* `+0xf78` in the save file (`MM:SS:ff`)
The timer consists of two components. The `HH` component keeps track of the hour. It is assigned by the following instruction:
```
801e6ea4 li      $v0, 0x0003 ; set 3 as the number of hours required to wait between Celerity uses
```
The code can be found at `BIN/BMAGIC/MAGIC110.EMI: 00010ea4`.
The `MM:SS:ff` start counting down a few frames after the `HH` byte is assigned. 