Whether or not an attack lands is calculated after the actual damage calculation.
```
801def60 lbu    $s0, 0x0037(v0) ; load party member's accuracy
801def64 lbu    $v0, -0x1f40(v1)
801def68 addiu  $a0, 0x79b8
801def6c sll    $v1, $v0, 0x03
801def70 subu   $v1, $v0
801def74 sll    $v0, $v1, 0x04
801def78 subu   $v0, $v1
801def7c sll    $v0, 0x02
801def80 addu   $a0, $v0, $a0
801def84 lbu    $v1, 0x0120(a0)
801def88 li     $v0, 0x0008
801def8c bne    $v1, $v0, 0x801defd4
801def90 lui    $v0, 0x8012
801defd4 lw     $v0, -0x1f34(v0)
801defd8 nop    
801defdc lhu    $v1, 0x00ae(v0)
801defe0 nop    
801defe4 andi   $v0, $v1, 0x0001
801defe8 beqz   $v0, 0x801deff4
801defec andi   $v0, $v1, 0x0004
801deff4 beqz   $v0, 0x801df00c
801deff8 sll    $v0, $s0, 0x10
801df00c jal    0x8016f384 ; call random number generator
801df010 nop    
...
801df014 lui    $v1, 0x51eb
801df018 ori    $v1, 0x851f
801df01c mult   $v0, $v1
801df020 sra    $v1, $v0, 0x1f
801df024 mfhi   $a1, $hi
801df028 sra    $a0, $a1, 0x05
801df02c subu   $a0, $v1
801df030 sll    $v1, $a0, 0x01
801df034 addu   $v1, $a0
801df038 sll    $v1, 0x03
801df03c addu   $v1, $a0
801df040 sll    $v1, 0x02
801df044 subu   $v0, $v1 ; get a random number between 0 and 99
801df048 sll    $v1, $s0, 0x10
801df04c sra    $v1, 0x10
801df050 subu   $v0, $v1 ; subtract accuracy from the random npumber
801df054 not    $v0 ; flip the sign of the result
801df058 srl    $v0, 0x1f ; get the sign
801df05c lw     $ra, 0x0014(sp)
801df060 lw     $s0, 0x0010(sp)
801df064 jr     $ra
801df068 addiu  $sp, 0x0018
801d9440 andi   $v0, 0x00ff
801d9444 beqz   $v0, 0x801d9490
801d9448 nop
; if the sign is positive then land the hit
801d9490 jal    0x801d52d4
```
This code can be found at `BIN/BATTLE/BTLMOVE.EMI: 00016f60`