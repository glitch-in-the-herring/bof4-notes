| Armor ID     | Equipability | Weight | Defense |
| ------------ | ------------ | ------ | ------- |
| `0x40`<br>64 | Ershin       | 5      | 30      |
The Spirit Armor adds 10 to the user's WIS
```
80193c0c lhu    $v0, 0x0048(s0) ; load current WIS
80193c10 nop    
80193c14 addiu  $v0, 0x000a ; add 10 to WIS
80193c18 j      0x80193c70
80193c1c sh     $v0, 0x0048(s0) ; store new WIS
```
The code can be found at `BIN/SYSTEM/GAME.EMI: 00006c0c`