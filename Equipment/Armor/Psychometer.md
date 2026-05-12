| Armor ID     | Equipability | Weight | Defense |
| ------------ | ------------ | ------ | ------- |
| `0x39`<br>57 | Ershin       | 5      | 20      |
The Psychometer adds 20 WIS to the user
```
80193b88 lhu    $v0, 0x0048(s0) ; load current WIS
80193b8c nop    
80193b90 addiu  $v0, 0x0014 ; add 20 to the current WIS
80193b94 j      0x80193c70
80193b98 sh     $v0, 0x0048(s0) ; store new WIS
```
This code can be found at `BIN/SYSTEM/GAME.EMI: 00006b88`