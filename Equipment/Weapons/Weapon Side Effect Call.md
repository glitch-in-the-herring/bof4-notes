A weapon side effect call is a function that is called when a weapon is equipped. 
```
80196374 move   $a0, $s0
801937fc addiu  $sp, -0x0018
80193800 sw     $s0, 0x0010(sp)
80193804 move   $s0, $a0
80193808 sw     $ra, 0x0014(sp)
8019380c lbu    $v0, 0x0080(s0) ; load weapon's ID
80193810 nop    
80193814 addiu  $v1, $v0, -0x0009 ; offset ID by -9: the first weapon to have a side effect is the Broad Sword, whose ID is 0x09
80193818 sltiu  $v0, $v1, 0x003b ; 
8019381c beqz   $v0, 0x80193940
80193820 lui    $v0, 0x8019
; if the weapon's ID is below 0x44 (Red Knuckles), all weapons with ID greater than or equal to 0x44 has no side effects
80193824 addiu  $v0, -0x2778 ; get the base address for weapon side effect calls
80193828 sll    $v1, 0x02 ; multiply offset by 4
8019382c addu   $v1, $v0 ; add offset to base address
80193830 lw     $v0, 0x0000(v1) ; load the side effect call's address
80193834 nop    
80193838 jr     $v0 ; execute side effect call
8019383c nop    
```
This code can be found at `BIN/SYSTEM/GAME.EMI: 00009374`.