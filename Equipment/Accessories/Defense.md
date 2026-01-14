Some accessories serve as secondary pieces of armor, in that they add to the wearer's defense.
The following code can be found at `BIN/SYSTEM/GAME.EMI: 00009434`.
```
80196434 lbu     $a0, 0x0082(s0) ; load the character's accessory
80196438 addiu   $v1, -0x5694 ; load the base address of the accessory general table 
8019643c sll     $v0, $a0, 0x01 ; multiply the accessory id by 2
80196440 addu    $v0, $a0  ; multiply the accessory id by 3
80196444 sll     $v0, 0x02  ; multiply the accessory id by 12
80196448 addu    $v0, $v1  ; offset + base address
8019644c lhu     $v1, 0x0044(s0) ; load the character's defense
80196450 lhu     $v0, 0x0006(v0) ; load the accessory's defense
80196454 nop     
80196458 addu    $v1, $v0 ; add the accessory's defense to the character's defense
8019645c sh      $v1, 0x0044(s0) ; store the new defense
```