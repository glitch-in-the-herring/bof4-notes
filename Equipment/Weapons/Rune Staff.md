| ID           | Equipped By | Element | Weight | Power | Hits | Shield Damage |
| ------------ | ----------- | ------- | ------ | ----- | ---- | ------------- |
| `0x27`<br>39 | Nina        | None    | 2      | 72    | 1    | 1             |
The Rune Staff adds 5 to the user's CP and 10 to the user's Wisdom.
```
801938b8 lhu    $v0, 0x0040(s0) ; load user's CP
801938bc lhu    $v1, 0x0048(s0) ; load user's WIS
801938c0 addiu  $v0, 0x0005 ; add 5 to CP
801938c4 addiu  $v1, 0x000a ; add 10 to WIS
801938c8 sh     $v0, 0x0040(s0) ; store new CP
801938cc j      0x80193940
801938d0 sh     $v1, 0x0048(s0) ; store new WIS
```
This code can be found at `BIN/SYSTEM/GAME.EMI: 000068b8`.