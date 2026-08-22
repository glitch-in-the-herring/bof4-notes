| Armor ID     | Equipability | Weight | Defense |
| ------------ | ------------ | ------ | ------- |
| `0x26`<br>38 | Nina         | 4      | 50      |
The Sage's Frock gives the user +5 Wisdom.
```
80193ad8 lhu    $v0, 0x0048(s0) ; load the user's current WIS
80193adc nop    
80193ae0 addiu  $v0, 0x0005 ; add 5 to WIS
80193ae4 j      0x80193c70
80193ae8 sh     $v0, 0x0048(s0) ; store new WIS
```
The code can be found at `BIN/SYSTEM/GAME.EMI: 00006ad8`.