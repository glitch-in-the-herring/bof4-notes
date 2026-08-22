An armor side effect call is a function that is called when an armor is equipped. The base address for the functions is 
* `0x8018d978` in the RAM
* `BIN/SYSTEM/GAME.EMI: 00000978` in the game's files
```
80193960 lbu    $v0, 0x0081(s0) ; load armor's ID
80193964 nop    
80193968 addiu  $v1, $v0, -0x000a ; offset ID by -10: the first armor to have a side effect is the Magma Armor, whose ID is 0x0a
8019396c sltiu  $v0, $v1, 0x003c
80193970 beqz   $v0, 0x80193c70
80193974 lui    $v0, 0x8019
; if the ID is less than 0x46
80193978 addiu  $v0, -0x2688 ; get the base address for armor side effect calls
8019397c sll    $v1, 0x02 ; multiply offset by 4
80193980 addu   $v1, $v0 ; add offset to base address
80193984 lw     $v0, 0x0000(v1) ; load the side effect call's addres
80193988 nop    
8019398c jr     $v0 ; execute the side effect call
```
This code can be found at `BIN/SYSTEM/GAME.EMI: 00006960`.