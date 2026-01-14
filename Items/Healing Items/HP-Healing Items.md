## Field
The following code can be found at `BIN/SYSTEM/SGAMEN.EMI: 0003015c`.
```
801aa95c lw     $a1, 0x0038(a0) ; load the character's current max HP
...
801aa968 lui    $v1, 0x801a
801aa974 lui    $v0, 0x8012
801aa978 lbu    $v0, -0x56f1(v0) ; load the ID of the item
801aa97c addiu  $v1, -0x6264 ; load base address of the items general table
801aa980 sll    $v0, 0x03 ; multiply ID by 8
801aa984 addu   $v0, $v1 ; offset + base address
801aa988 lbu    $v1, 0x0003(v0) ; load item's power
801aa98c li     $v0, 0x00ff
801aa990 beq    $v1, $v0, 0x801aa9ac
    ; If the item heals HP completely
    801a9ac sw      $a1, 0x0014(a0) ; set current HP to max HP
    
    ; If the item does not heal HP completely
    801aa994 sll    $v0, $v1, 0x02 ; multiply power by 4
    801aa998 addu   $v0, $v1 ; multiply power by 5
    801aa99c sll    $v0, 0x01 ; multiply power by 10
    801aa9a0 addu   $v0, $a2, $v0 ; add 10 * power to the current HP
    801aa9a4 j      0x801aa9b0
    801aa9a8 sw     $v0, 0x0014(a0) ; store HP
```
## Battle
The following code can be found at `BIN/BATTLE/BTLMOVE.EMI: 00011c9c`
```
...
801d9c9c lbu     $v0, 0x0001(s1) ; load the ID of the item
801d9ca0 nop     
801d9ca4 beq     $v0, $r0, 0x801d9d24
801d9ca8 li      $v0, 0x00ff
801d9cac lbu     $v1, 0x0002(s1) ; load the power of the item
801d9cb0 nop     
801d9cb4 bne     $v1, $v0, 0x801d9cf0
801d9cb8 lui     $a0, 0x8012

	; If the item does not heal completely
	801d9cf0 sll     $v0, $v1, 0x02 ; multiply power by 4 
	801d9cf4 addu    $v0, $v1 ; multiply power by 5
	801d9cf8 sll     $v0, 0x01 ; multiply power by 10
	801d9cfc lw      $v1, -0x1ec0(a0) 
	801d9d00 subu    $v0, $r0, $v0 ; -10*power 
	801d9d04 sw      $v0, 0x000c(v1) ; store the healed amount

...
801d8f50 8c8300b0: lw     $v1, 0x00b0(a0) ; load the character's current HP
801d8f54 8c42000c: lw     $v0, 0x000c(v0) ; load the healed amount
801d8f58 00000000: nop    
801d8f5c 00621823: subu   $v1, $v0 ; add the healed amount to the character's HP
801d8f60 18600008: blez   $v1, 0x801d8f84
801d8f64 3c028012: lui    $v0, 0x8012
801d8f68 8c8400d4: lw     $a0, 0x00d4(a0) 
801d8f6c 00000000: nop    
801d8f70 0083102a: slt    $v0, $a0, $v1
801d8f74 10400004: beq    $v0, $r0, 0x801d8f88
801d8f78 3c028012: lui    $v0, 0x8012
801d8f88 8c42e13c: lw     $v0, -0x1ec4(v0)
801d8f8c 00000000: nop    
801d8f90 ac4300b0: sw     $v1, 0x00b0(v0) ; store the character's new HP
```
