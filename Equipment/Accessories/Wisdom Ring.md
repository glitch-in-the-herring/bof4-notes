| Accessory ID | Equipped By | Weight | Defense |
| ------------ | ----------- | ------ | ------- |
| `0x0d`<br>13 | All         | 2      | 3       |
The Wisdom Ring increases the wearer's WIS by 20 points.
```
80193d04 lhu    $v0, 0x0048(s0) ; load current WIS
80193d08 nop    
80193d0c addiu  $v0, 0x0014 ; add 20 to WIS
80193d10 j      0x80193f0c
80193d14 sh     $v0, 0x0048(s0) ; store WIS
```
This code can be found at `BIN/SYSTEM/GAME.EMI: 00006d04` in the game's files