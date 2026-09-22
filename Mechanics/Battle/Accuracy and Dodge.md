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
## Frequent Dodges
The frequent dodges flag on an enemy causes the attacker to miss 70% of their attacks if they are not blind, 35% if they are.
```
801ded60 lhu    $v0, 0x00ac(v0) ; load enemy's behavior
801ded64 nop    
801ded68 andi   $v0, 0x2000
801ded6c beqz   $v0, 0x801ded78 
801ded70 move   $s0, $r0

; if the enemy has frequent dodges
801ded74 li     $s0, 0x0046 ; dodge rate
801ded78 lui    $v0, 0x8012
801ded7c addiu  $a0, $v0, -0x1ed0
801ded80 lw     $v0, 0x000c(a0)
801ded84 nop    
801ded88 lhu    $v1, 0x00ae(v0) ; load enemy's status
801ded8c nop    
801ded90 andi   $v0, $v1, 0x0004 ; check for blind status
801ded94 beqz   $v0, 0x801deda0
801ded98 andi   $v0, $s0, 0xffff

; if the enemy is blind
801ded9c srl    $s0, $v0, 0x01 ; reduce dodge chance by 50%

801deda0 lw     $v0, 0x0010(a0)
801deda4 nop    
801deda8 lhu    $v0, 0x0000(v0)
801dedac nop    
801dedb0 andi   $v0, 0x0001
801dedb4 beqz   $v0, 0x801dee00
801dedb8 andi   $v0, $v1, 0x4000
801dee00 jal    0x8016f384 ; go to random number function
801dee04 nop    
8016f384 li     $t2, 0x00a0
8016f388 jr     $t2
8016f38c li     $t1, 0x002f
...
801dee08 lui    $v1, 0x51eb
801dee0c ori    $v1, 0x851f
801dee10 mult   $v0, $v1 
801dee14 sra    $v1, $v0, 0x1f
801dee18 mfhi   $a3, $hi
801dee1c sra    $a0, $a3, 0x05
801dee20 subu   $a0, $v1
801dee24 sll    $v1, $a0, 0x01 
801dee28 addu   $v1, $a0
801dee2c sll    $v1, 0x03
801dee30 addu   $v1, $a0
801dee34 sll    $v1, 0x02
801dee38 subu   $v0, $v1 ; get a random number from 0 to 99
801dee3c andi   $v1, $s0, 0xffff
801dee40 subu   $v0, $v1 ; subtract dodge rate from roll
801dee44 bgez   $v0, 0x801deec8 
801dee48 move   $v0, $r0
; if the result is negative, then the attack is dodged
801dee4c lui    $v1, 0x8012
```
This code can be found at `BIN/BATTLE/BTLMOVE.EMI: 00016d60`.
## Dodging (Player Party)
The code that checks for a player party character dodging a hit is only slightly different with the enemy code above:
```

```