Whether or not a physical attack (melee or ranged) is a critical hit is determined a few frames before the [[Melee Formula]] is called.
```
801df5e8 lbu    $v1, 0x011c(v0) ; load user's weapon
801df5ec li     $v0, 0x004f 
801df5f0 bne    $v1, $v0, 0x801df638
801df5f4 lui    $v0, 0x8012
; if the weapon is not a Power Glove
801df638 jal    0x8016f384 ; call the random number function
801df63c nop    
...
801df640 lui    $v1, 0x51eb
801df644 ori    $v1, 0x851f
801df648 mult   $v0, $v1
801df64c sra    $v1, $v0, 0x1f
801df650 mfhi   $a2, $hi
801df654 sra    $a0, $a2, 0x05
801df658 subu   $a0, $v1
801df65c sll    $v1, $a0, 0x01
801df660 addu   $v1, $a0
801df664 sll    $v1, 0x03
801df668 addu   $v1, $a0
801df66c sll    $v1, 0x02
801df670 lui    $a0, 0x8012
801df674 addiu  $a1, $a0, -0x1f40
801df678 lbu    $a0, 0x0034(a1) ; load party member's critical rate
801df67c subu   $v0, $v1 ; get a random number from 0 99
801df680 subu   $v0, $a0
801df684 bgez   $v0, 0x801df700
801df688 lui    $v0, 0x8012
; if random number - critical rate is negative
801df68c lw     $a0, 0x0010(a1)
801df690 nop    
801df694 lhu    $v1, 0x0000(a0) ; load the attack flag
801df698 li     $v0, 0x0001
801df69c j      0x801df714
801df6a0 ori    $v1, 0x0004 ; set the critical bit
801df714 sh     $v1, 0x0000(a0) ; store the attack flag
```
This code can be found at `BIN/BATTLE/BTLMOVE.EMI: 000175e8`