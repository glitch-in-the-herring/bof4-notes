| Spell ID      | Targeting                  | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | -------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x8e`<br>142 | Single<br>Enemy party only | Yes<br>1  | 0<br> | 1   | Status  | LV DWN    |
Covers target in oil, ~~making them able to fly in the rain~~ making their fire resistance 0. Sequelae are blocked. It is the only spell that uses the LV DWN icon.

* As a standalone spell, the stat change data can be found at:
	* `BIN/BMAGIC/MAGIC142.EMI: 00015e98` in the files
	* `0x801e7698`in the RAM 
	* Normally targets the fire resistance
* The first sequela's stat change data can be found at:
	* `BIN/BMAGIC/MAGIC142.EMI: 00015e9c` in the files
	* `0x801e769c`in the RAM 
	* Normally targets the fire resistance but is blocked
* The second sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC142.EMI: 00015ea0` in the files
	* `0x801e76a0`in the RAM 
	* Normally targets the fire resistance but is blocked
* The third sequela's stat change data can be found at
	* `BIN/BMAGIC/MAGIC142.EMI: 00015ea4` in the files
	* `0x801e76a4`in the RAM 
	* Normally targets the fire resistance but is blocked

The following code can be found at `BIN/SYSTEM/GAME.EMI: 00009ae0`.
```
80196ae0 sb     $r0, 0x00ea(s0) ; sets the target's fire resistance to 0
```
It uses the [[General Success Rate Formula]] to determine whether or not the spell hits. Its primary element is Status, and its secondary element is Magic