## Learning Roll
When a character is guarding, they are able to learn certain spells used by the enemy or an ally. The success rate of this mechanic is determined by:
$$
r = \begin{cases}
\mathrm{random}(0, 9999) - \frac{100}{d}\left(\frac{100\alpha}{AP_{max}} + \ell + 100\right) & \text{Not apprenticed to the Abbess}\\
\mathrm{random}(0, 9999) - \frac{100}{d}\left(\frac{100\alpha}{AP_{max}} + \ell + 175\right) & \text{Apprenticed to the Abbess}\\
\end{cases}
$$
$$
\begin{cases}
\mathrm{success} & r <0\\
\mathrm{fail} & r \geq0
\end{cases}
$$
$\ell$ = Character's learning rate.
$\alpha$ = Unknown 16-bit term, appears to be 0 in most cases.
$d$ = Difficulty of learning the spell, obtained by looking at the second digit of the 2nd position byte of the spell in the [[Spells/General Table|General Table]]:

| Difficulty | $d$ |
| ---------- | --- |
| 1          | 1   |
| 2          | 2   |
| 3          | 4   |
| 4          | 8   |
| 5          | 12  |
| 5          | 16  |
| 6          | 32  |
| 7          | 64  |
This table is located at:
* `0x801cc834` in the RAM
* `BIN/BATTLE/BTLMOVE.EMI: 00004834` in the game's files
This is a competitive process: The first party member with a negative $r$ gets the spell. If that party member's skill slots are full, then they are skipped. 
The learning rate can be found:
- `+0xf2` from the start of the true start of the character's section
- `+0x56` from the character's name
### Code
```
; ; ; ; ; ; ; ; ; ; ; ; ;
; Unknown stat alpha    ;
; ; ; ; ; ; ; ; ; ; ; ; ;
801d8320 lhu     $v1, 0x00b8(s1) ; load alpha, a stat whose purpose is unknown
801d8324 nop     
801d8328 sll     $v0, $v1, 0x01 ; multiply alpha by 2
801d832c addu    $v0, $v1 ; multiply alpha by 3
801d8330 sll     $v0, 0x03 ; multiply alpha by 24
801d8334 addu    $v0, $v1 ; multiply alpha by 25
801d8338 lw      $v1, 0x00d8(s1) ; load the max AP of the character
801d833c sll     $v0, 0x02 ; multiply alpha by 100
801d8340 divu    $v0, $v1 ; divide  alpha * 100 by the max AP of the character
801d8344 bne     $v1(000001ea), $r0(00000000), 0x801d8350
801d8348 nop    
; If a division by zero happens
	801d834c break   0x0007 ; throw an error

801d8350 mflo    $s0(00000659), $lo(00000000)
801d8354 nop    
801d8358 slti    $v0, $s0, 0x001a
801d835c bne     $v0, $r0, 0x801d8368
801d8360 nop    
; If alpha * 100 / max AP is more than or equal to 26
	801d8364 li      $s0, 0x0019 ; cap it to 25. We'll call this the modifier for now.
```

```
801d8368 lbu     $v1, 0x0120(s1) ; load the character's master
801d836c li      $v0, 0x0004 ; the Abbess' ID is 4
801d8370 bne     $v1, $v0, 0x801d8390
801d8374 nop    
; If the character's master is the Abbess
    801d8378 lbu     $v0, 0x00a4(s1) ; load k, another unknown stat
    801d837c nop    
    801d8380 sltiu   $v0, 0x0007
    801d8384 beq     $v0, $r0, 0x801d8390 
    ; If k is greater than 7
	    801d8388 nop     ; do thing
	; If k is less than 7
	    801d838c addiu   $s0, 0x004b ; add 75 to the modifier.

801d8390 lbu     $v0, 0x00f2(s1) ; load the character's learning rate
801d8394 lw      $a0, 0x00d8(s1) ; load the character's max AP
801d8398 lhu     $a1, 0x00b8(s1) ; load alpha
801d839c addu    $s0, $v0 ; add the modifier to the character's learning rate
801d83a0 addiu   $s0, 0x0064 ; add 100 to the above. Let this be the total learning rate
801d83a4 sll     $v1, $s0, 0x01 ; multiply the total learning rate by 2
801d83a8 addu    $v1, $s0 ; multiply the total learning rate by 3
801d83ac sll     $v1, 0x03 ; multiply the total learning rate by 24
801d83b0 addu    $v1, $s0 ; multiply the total learning rate by 25
801d83b4 sll     $v0, $s4, 0x01 ; multiply the current spell's ID by 2
801d83b8 addu    $v0, $s4 ; multiply the current spell's ID by 3
801d83bc sll     $v0, 0x02 ; multiply the current spell's ID by 12
801d83c0 addu    $v0, $s7 ; add the above as an offset for the general spell table
801d83c4 lbu     $v0, 0x0002(v0) ; load the spell's difficulty
801d83c8 sll     $s0, $v1, 0x02 ; multiply the total learning rate by 100
801d83cc andi    $a2, $v0, 0x000f ; take only the last digit of the difficulty
801d83d0 srl     $v0, $a0, 0x02 ; divide the max AP by 4
801d83d4 sltu    $v0, $a1, $v0 
801d83d8 bne     $v0, $r0, 0x801d83e4
801d83dc addiu   $v1, $a2, -0x0001 ; the difficulty starts at 1. a difficulty of 0 means the spell cannot be learned.
; If alpha is more than max AP / 4
	801d83e0 addiu   $v1, $a2, -0x0002 ; decrement the difficulty by 2
	
801d83e4 srl     $v0, $a0, 0x01 ; divide the max AP by 2
801d83e8 sltu    $v0, $a1, $v0
801d83ec bne     $v0, $r0, 0x801d83f8
801d83f0 nop    
; If alpha is more than max AP / 2
	801d83f4 addiu   $v1, -0x0001 ; decrement the difficulty by 1
	
801d83f8 bgez    $v1, 0x801d8408
801d83fc addu    $v0, $sp, $v1 ; add the diffculty as an offset to the d-table
; If the difficulty is negative
	801d8400 move    $v1, $r0 ; set the difficulty so that it cannot be lower than 0
	801d8404 addu    $v0, $sp, $v1 ; add the diffculty as an offset to the d-table
	
801d8408 lbu     $v0, 0x0010(v0) ; load the d-value
801d840c nop    
801d8410 div     $s0, $v0 ; divide total learning rate * 100 by the difficulty
801d8414 bne     $v0, $r0, 0x801d8420
801d8418 nop    
; If a division by zero happens
	801d841c break   0x0007 ; throw an error
	
801d8420 li      $at, -0x0001
801d8424 bne     $v0, $at, 0x801d8438 
801d8428 lui     $at, 0x8000
801d8438 mflo    $s0, $lo
801d843c jal     0x8016f384 ; call the rand() function
...
801d8444 lui     $v1, 0x68db
801d8448 ori     $v1, 0x8bad
801d844c mult    $v0, $v1 ; divide the random number by 10000
801d8450 mfhi    $v1, $hi
801d8454 sra     $a0, $v1, 0x0c
801d8458 sra     $v1, $v0, 0x1f 
801d845c subu    $a0, $v1
801d8460 sll     $v1, $a0, 0x02 ; multiply by 4
801d8464 addu    $v1, $a0 ; multiply by 5
801d8468 sll     $v1, 0x03 ; multiply by 40
801d846c subu    $v1, $a0 ; multiply by 39
801d8470 sll     $v1, 0x04 ; multiply by 624
801d8474 addu    $v1, $a0 ; multiply by 625
801d8478 sll     $v1, 0x04 ; multiply by 10000, rounding down the random number to the smallest multiple of 10000
801d847c subu    $v0, $v1 ; gets a random number from 0 to 9999
801d8480 subu    $v0, $s0 ; calculate r
801d8484 bgez    $v0, 0x801d84a4 
```