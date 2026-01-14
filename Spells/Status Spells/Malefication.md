| Spell ID      | Targeting                 | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | ------------------------- | --------- | ----- | --- | ------- | --------- |
| `0xce`<br>206 | All<br>Always enemy party | No        | 0     | 0   | Status  | Normal    |
Malefication is a status spell that induces poison and blindness on all of its targets. It uses the [[General Success Rate Formula]] to determine the chance of a target being affected.
Its primary element is Status, and is set by the following code:
```
801da33c li      $a0, 0x0006 ; load status
```
It can be found at `BIN/BATTLE/BTLMOVE.EMI: 0001233c`. It is shared by:
* [[Chlorine]]
* [[Spores]]
* [[Flex]]