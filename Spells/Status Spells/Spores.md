| Spell ID      | Targeting                 | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | ------------------------- | --------- | ----- | --- | ------- | --------- |
| `0xc0`<br>192 | All<br>Always enemy party | Np        | 0     | 0   | Status  | Normal    |
Spores is a status effect used by Rafresia and Sporeon. It induces Euphoria on its target. 
Its primary element is Status and is set by the following code:
```
801da33c li      $a0, 0x0006 ; load status
```
It can be found at `BIN/BATTLE/BTLMOVE.EMI: 0001233c`. It is shared by:
* [[Chlorine]]
* [[Flex]]
* [[Malefication]]