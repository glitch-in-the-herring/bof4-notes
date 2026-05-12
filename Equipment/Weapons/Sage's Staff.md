| ID           | Equipped By | Element | Weight | Power | Hits | Shield Damage |
| ------------ | ----------- | ------- | ------ | ----- | ---- | ------------- |
| `0x21`<br>33 | Nina        | None    | 2      | 12    | 1    | 1             |
Sage's Staff adds +5 to the user's WIS
```
8019387c lhu    $v0, 0x0048(s0) ; load current WIS
80193880 nop    
80193884 addiu  $v0, 0x0005 ; add 5 to current WIS
80193888 j      0x80193940
8019388c sh     $v0, 0x0048(s0) ; store new WIS
```
This code can be found at `BIN/SYSTEM/GAME.EMI: 0000687c` in the game's files