| Spell ID     | Targeting                  | Learnable | Power | AP  | Element | Icon/Type       |
| ------------ | -------------------------- | --------- | ----- | --- | ------- | --------------- |
| `0x5f`<br>95 | Single<br>Enemy party only | Yes<br>3  | 0     | 2   | Status  | Melee<br>Status |
Chlorine is a melee attack that has a chance to poison the target. It uses the [[General Success Rate Formula]] to determine whether or not the attack inflicts poison on its target.
Its primary resistance is Status, and is set by the following code:
```
801da33c li      $a0, 0x0006 ; load status
```
It can be found at `BIN/BATTLE/BTLMOVE.EMI: 0001233c`. It is shared by:
* [[Flex]]
* [[Spores]]
* [[Malefication]]