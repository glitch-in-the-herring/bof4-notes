| ID           | Equipped By   | Element | Weight | Power | Hits | Shield Damage |
| ------------ | ------------- | ------- | ------ | ----- | ---- | ------------- |
| `0x16`<br>22 | Ryu<br>Fou-lu | None    | 2      | 90    | 1    | 6             |
The cursed sword multiplies melee damage up to 2x, scaled according to how much HP the user has left:

$$
d'=\left\lfloor\frac{2HP\cdot d}{MHP}\right\rfloor
$$

```
801d3ca4 lbu    $a1, 0x011c(v1) ; load weapon ID
...
801d3d20 li     $v0, 0x0016
801d3d24 bne    $a0, $v0, 0x801d3d88
801d3d28 li     $v0, 0x0039
; if the weapon is a Cursed Sword
801d3d2c lui    $v1, 0x8012
801d3d30 addiu  $v1, -0x1f40
801d3d34 lw     $v0, 0x000c(v1)
801d3d38 nop    
801d3d3c lw     $v0, 0x00b0(v0) ; load current HP
801d3d40 nop    
801d3d44 sll    $v0, 0x01 ; current HP * 2
801d3d48 mult   $s0, $v0 ; multiply base damage by current HP * 2
801d3d4c mflo   $a2, $lo
801d3d50 lw     $v0, 0x0014(v1) ; load current max HP
801d3d54 nop    
801d3d58 div    $a2, $v0 ; divide base damage by current HP * 2, the new damage is base damage * 2 * (current HP / current max AP)
```