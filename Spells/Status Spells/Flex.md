| Spell ID      | Targeting                             | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | ------------------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x9e`<br>158 | All<br>Enemy and player party (front) | No        | 0     | 0   | Status  | Status    |
Flex is a spell that poisons the entire enemy party and the front row of the player's party. It uses the [[General Success Rate Formula]] to determine the chance of a target being poisoned.

* As a standalone spell, the status change data can be found at:
	* `BIN/BMAGIC/MAGIC158.EMI: 00012d24` in the files
	* `0x801e6d24`in the RAM 
* The first sequela's status change data can be found at:
	* `BIN/BMAGIC/MAGIC158.EMI: 00012d28` in the files
	* `0x801e6d28`in the RAM 
	* Normally blocked
* The second sequela's status change data can be found at
	* `BIN/BMAGIC/MAGIC158.EMI: 00012d2c` in the files
	* `0x801e6d2c`in the RAM 
	* Normally blocked

Its primary element is Status, and is set by the following code:
```
801da33c li      $a0, 0x0006 ; load status
```
It can be found at `BIN/BATTLE/BTLMOVE.EMI: 0001233c`. It is shared by:
* [[Chlorine]]
* [[Spores]]
* [[Malefication]]