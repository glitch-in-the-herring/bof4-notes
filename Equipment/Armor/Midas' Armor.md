| Armor ID     | Equipability                   | Weight | Defense |
| ------------ | ------------------------------ | ------ | ------- |
| `0x2e`<br>46 | Ryu<br>Cray<br>Scias<br>Fou-Lu | 2      | 25      |
Midas' Armor turns 2% of damaged received + 25 to zenny.
```
801d9608 lbu    $v1, 0x011d(v0) ; load armor ID
801d960c li     $v0, 0x002e
801d9610 bne    $v1, $v0, 0x801d9688
801d9614 move   $v0, $s0
; if the armor is Midas' Armor
801d9618 lw     $v0, 0x0010(a1) ; load HP-AP change location
801d961c nop    
801d9620 lw     $a0, 0x000c(v0) ; load damage 
801d9624 nop    
801d9628 blez   $a0, 0x801d9660
801d962c lui    $v0, 0x51eb
 ; if the damage is greater than zero
801d9630 ori    $v0, 0x851f
801d9634 addiu  $a0, 0x0019 ; add 25 to the damage
801d9638 mult   $a0, $v0
801d963c lui    $a1, 0x8012
801d9640 addiu  $a1, -0x20d0
801d9644 sra    $a0, 0x1f
801d9648 lw     $v0, 0x001c(a1)
801d964c mfhi   $a3, $hi
801d9650 sra    $v1, $a3, 0x04 ; multiply damage + 25 by 2%, this is the zenny received from the damage
801d9654 subu   $v1, $a0
801d9658 addu   $v0, $v1 ; add the zenny received to the total zenny payout
801d965c sw     $v0, 0x001c(a1) ; store new zenny payout
```