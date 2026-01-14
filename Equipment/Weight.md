All equipment have weight. This reduces the character's agility. The calculation that subtracts the weight from the character's agility is the same for all three types of equipment.
The following code can be found at `BIN/SYSTEM/GAME.EMI: 0000674c`
```
8019374c lui     $v0, 0x801a
80193750 lbu     $a0, 0x0080(a2) ; load the character's weapon
80193754 addiu   $v0, -0x5eac ; load the base address of the weapons general table
80193758 sll     $v1, $a0, 0x03 ; multiply the weapon id by 8
8019375c subu    $v1, $a0 ; multiply the weapon id by 7
80193760 sll     $v1, 0x01 ; multiply the weapon id by 7
80193764 addu    $v1, $v0 ; offset + base address
80193768 lbu     $a1, 0x0006(v1) ; load the weight of the weapon
8019376c lbu     $v0, 0x0081(a2) ; load the character's armor
80193770 nop     
80193774 beq     $v0, $r0, 0x801937a0
80193778 lui     $v1, 0x801a

; If the character is not equipped with a piece of armor

; If the character is equipped with a piece of armor
8019377c move    $a0, $v0 ; move $v0 to $a0
80193780 addiu   $v1, -0x59dc ; load the base address of the armor general table
80193784 sll     $v0, $a0, 0x01 ; multiply the armor id by 2
80193788 addu    $v0, $a0 ; multiply the armor id by 3
8019378c sll     $v0, 0x02 multiply the armor id by 12
80193790 addu    $v0, $v1 ; offset + base address
80193794 lbu     $v0, 0x0005(v0) ; load the weight of the armor
80193798 nop     
8019379c addu    $a1, $v0 ; add the armor weight to the total weight
801937a0 lbu     $v0, 0x0082(a2) ; load the character's accessory
801937a4 nop     
801937a8 beq     $v0, $r0, 0x801937d4 
801937ac lui     $v1, 0x801a

; If the character is not equipped with a piece of accessory

; If the character is equipped with a piece of accessory
801937b0 move    $a0, $v0 ;move $v0 to $a0
801937b4 addiu   $v1, -0x5694 ; load the base address of the accessory general table
801937b8 sll     $v0, $a0, 0x01 ; multiply the accessory id by 2 
801937bc addu    $v0, $a0 ; multiply the accessory id by 3
801937c0 sll     $v0, 0x02 ; multiply the accessory id by 12
801937c4 addu    $v0, $v1 ; offset + base address
801937c8 lbu     $v0, 0x0005(v0) ; load the weight of the accessory
801937cc nop     
801937d0 addu    $a1, $v0 ; add the accessory weight to the total weight
801937d4 lhu     $v0, 0x0046(a2) ; load the character's current agility
801937d8 nop     
801937dc subu    $v0, $a1 ; subtract the total weight from the character's agility
801937e0 sh      $v0, 0x0046(a2) ; store the new agility
```