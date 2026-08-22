An accessory side effect call is a function that is called when an accessory is equipped. The base address for the functions is 
* `0x8018da68` in the RAM
* `BIN/SYSTEM/GAME.EMI: 00000a68` in the game's files
```
80193c90 lbu    $v0, 0x0082(s0) ; load accessory's ID
80193c94 nop    
80193c98 addiu  $v1, $v0, -0x0007 ; offset by -7: the first piece of accessory to have a side effect is the Divine Helm, whose ID is 0x07
80193c9c sltiu  $v0, $v1, 0x0030
80193ca0 beqz   $v0, 0x80193f0c
80193ca4 lui    $v0, 0x8019
; if the ID is less than 0x37
80193ca8 addiu  $v0, -0x2598 ; load base address for accessory side effect calls
80193cac sll    $v1, 0x02 ; multiply offset by 4
80193cb0 addu   $v1, $v0 ; add offset to base address
80193cb4 lw     $v0, 0x0000(v1) ; load side effect call's address
80193cb8 nop    
80193cbc jr     $v0 ; execute the side effect
```
The code can be found at `BIN/SYSTEM/GAME.EMI: 00006c90`