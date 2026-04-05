
| ID           | Equipped By | Element | Weight | Power | Hits | Shield Damage |
| ------------ | ----------- | ------- | ------ | ----- | ---- | ------------- |
| `0x4d`<br>77 | Ershin      | None    | 1      | 85    | 1    | 2             |
The Ghostbuster gives an extra 50% damage if the target is a Demon.
```
801d3ca4 lbu    $a1, 0x011c(v1) ; load weapon's ID
...
801d3cc8 li     $v0, 0x004d ; load ghostbuster's ID
801d3cf0 bne    $a1, $v0, 0x801d3d20
801d3cf4 andi   $a0, $a1, 0x00ff
801d3cf8 lui    $v0, 0x8012
801d3cfc lw     $v0, -0x1ec4(v0)
801d3d00 nop    
801d3d04 lbu    $v1, 0x0002(v0) ; load enemy's type
801d3d08 li     $v0, 0x0006 ; load the Demon type's ID
801d3d0c bne    $v1, $v0, 0x801d3d24
801d3d10 li     $v0, 0x0016
;if the enemy is a Demon
801d3d14 sra    $v0, $s0, 0x01 ; divide damage by 2
801d3d18 addu   $s0, $v0 ; multiply damage by 3/2
```
The code above can be found at `BIN/BATTLE/BTLMOVE.EMI: 0000bcc8`