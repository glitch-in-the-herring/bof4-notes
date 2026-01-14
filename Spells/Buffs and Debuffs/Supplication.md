| Spell ID      | Targeting | Learnable | Power | AP  | Element | Icon/Type      |
| ------------- | --------- | --------- | ----- | --- | ------- | -------------- |
| `0x6c`<br>108 | Self      | Yes<br>2  | 0<br> | 0   | None    | LV UP<br>ST UP |
Supplication is a buff that increases the user's holy resistance to 1 up to 6, and the user's dodge by 50pt.
The code can be found at `BIN/SYSTEM/GAME.EMI: 00009b34`
```
80196b34 li      $a0, 0x0001 ; load 1 to $a0
80196b38 jal     0x801946e8
80196b3c addiu   $a1, $s0, 0x00ee ; get the address of the user's holy resistance
801946e8 lbu     $v1, 0x0000(a1) ; load the user's holy resistance
801946ec li      $v0, 0x0007 ; load 7 to $v0
801946f0 beq     $v1, $v0, 0x8019472c
801946f4 move    $a2, $v1

; If the holy resistance is not already 7
801946f8 sll     $v0, $a0, 0x18
801946fc sra     $v0, 0x18
80194700 addu    $v1, $a2, $v0 ; add 1 to the user's holy resistance
80194704 slti    $v0, $v1, 0x0007
80194708 bne     $v0, $r0, 0x80194718
8019470c li      $v0, 0x0006 ; load 6 to $v0

; If the user's new holy resistance is greater than 6
80194710 jr      $ra
80194714 sb      $v0, 0x0000(a1) ; store 6 as the new resistance


; If the user's new holy resistance is less than 6
80194718 bgez    $v1, 0x80194728
8019471c addu    $v0, $a2, $a0
80194728 sb      $v0, 0x0000(a1) ; store the new holy resistance
...
80196b40 lbu     $v0, 0x00f5(s0) ; load the user's dodge
80196b44 nop    
80196b48 addiu   $v0, 0x0032 ; add 50 to the user's dodge
80196b4c sb      $v0, 0x00f5(s0) ; store the user's new dodge
```