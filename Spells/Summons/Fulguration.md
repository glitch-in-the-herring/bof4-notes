| Spell ID      | Targeting                 | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | ------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x48`<br> 72 | All<br>Always enemy party | No        | 0     | 0   | None    | Breath    |
Fulguration deals damage modified by the enemy's current HP and death resistance. The damage is calculated using the following formula:
$$
d=\left\lfloor\frac{CHP_D}{F}\right\rfloor
$$
Where $F$ is determined from the enemy's death resistance, a die roll, and current HP. If the enemy's HP is 1,000,000, then the enemy is invincible. If the enemy's death resistance multiplier is -1, then it is always 16. Otherwise, it is calculated by rolling:
$$
r = random(0,99) - \left\lfloor\frac{R_D\cdot100}{100}\right\rfloor
$$
$$
F=\begin{cases}
16 & r < 0\\
64 & r > 0
\end{cases}
$$
```
801df430 lbu    $v0, 0x002a(s0) ; load death res
801df434 addiu  $s1, $v1, 0x509c
801df438 sll    $v0, 0x01
801df43c addu   $v0, $s1
801df440 lh     $v1, 0x0040(v0) ; load death res multiplier
801df444 li     $v0, 0x00ff ;
801df448 beq    $v1, $v0, 0x801df4f4 
801df44c move   $s2, $a2
; if the death res multiplier is not -1
801df450 jal    0x8016f384 ; call random number function
801df454 nop    
...
801df458 lbu    $v1, 0x002a(s0) ; load death res
801df45c nop    
801df460 sll    $v1, 0x01
801df464 addu   $v1, $s1
801df468 lh     $v1, 0x0040(v1) ; load death res multiplier
801df46c andi   $a1, $s2, 0xffff
801df470 mult   $a1, $v1 ; multiply death res multiplier by 100
801df474 mflo   $a1, $lo
801df478 lui    $v1, 0x51eb
801df47c ori    $v1, 0x851f
801df480 mult   $v0, $v1
801df484 mfhi   $t0, $hi
801df488 nop    
801df48c nop    
801df490 mult   $a1, $v1
801df494 sra    $a0, $t0, 0x05
801df498 sra    $v1, $v0, 0x1f
801df49c subu   $a0, $v1
801df4a0 sll    $v1, $a0, 0x01
801df4a4 addu   $v1, $a0
801df4a8 sll    $v1, 0x03
801df4ac addu   $v1, $a0
801df4b0 sll    $v1, 0x02
801df4b4 subu   $v0, $v1 ; get random(0,99)
801df4b8 sra    $a1, 0x1f
801df4bc mfhi   $a2, $hi
801df4c0 sra    $v1, $a2, 0x05  ; divide death res multipler * 100 by 100
801df4c4 subu   $v1, $a1
801df4c8 subu   $v0, $v1 ; random(0,99) - death res multipler * 100 / 100
801df4cc bltz   $v0, 0x801df4f4 
801df4d0 andi   $v1, $s3, 0x00ff
; if the roll is positive
801df4d4 li     $v0, 0x0001 ; set the strong flag to active
801df4d8 bne    $v1, $v0, 0x801df4f8
801df4dc li     $a1, 0x0002

; if the roll is negative or if the death res multiplier is -1
801df4f4 move   $v0, $r0
801df4f8 lw     $ra, 0x0024(sp)
801df4fc lw     $s4, 0x0020(sp)
801df500 lw     $s3, 0x001c(sp)
801df504 lw     $s2, 0x0018(sp)
801df508 lw     $s1, 0x0014(sp)
801df50c lw     $s0, 0x0010(sp)
801df510 jr     $ra
801df514 addiu  $sp, 0x0028
801ddf08 andi   $v0, 0x00ff
801ddf0c beqz   $v0, 0x801ddf1c

; if the strong flag is active
801ddf10 li     $v0, 0x0040 ; load 64 as the factor

; if the strong flag is inactive
801ddf1c li     $v0, 0x0010 ; load 16 as the factor
801ddf20 j      0x801ddf40
801ddf24 sb     $v0, 0x0001(s2) ; store factor
```
This code can be found at `BIN/BATTLE/BTLMOVE.EMI: 00017430`