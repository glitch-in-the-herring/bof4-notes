Spells that have a chance of failing use this formula to determine their success:
$$
\begin{cases}
\mathrm{success} & r < 0\\
\mathrm{success} & (R_1 = 0)\vee(R_2 = 0)\\
\mathrm{fail} & r \geq 0\\
\mathrm{fail} & (R_1 \geq 6)\vee(R_1 \geq 6)\\
\mathrm{fail} & (RT_1 = \mathrm{Holy})\vee(R_1 \geq 5)
\end{cases}
$$
$$
r = \mathrm{random}(0, 99)-\beta
$$
$$\alpha_1 = \begin{cases}
\left\lfloor\frac{INT_{A}}{5}\right\rfloor + 50 & \left\lfloor\frac{INT_{A}}{5}\right\rfloor + 50 < 100\\
100 & \left\lfloor\frac{INT_{A}}{5}\right\rfloor + 50 \geq 100
\end{cases}
$$
$$
\alpha_2 = \begin{cases}
75 - \left\lfloor\frac{INT_{D}}{5}\right\rfloor  & 75 - \left\lfloor\frac{INT_{D}}{5}\right\rfloor \geq 25\\
25 & 75 - \left\lfloor\frac{INT_{D}}{5}\right\rfloor < 25
\end{cases}
$$
$$
\beta = \left\lfloor\frac{\left\lfloor\frac{\alpha_1\alpha_2}{100}\right\rfloor R_1R_2}{10000}\right\rfloor
$$

* $R_1$: Primary resistance multiplier
* $R_2$: Secondary resistance multiplier
The primary resistance's index starts at Fire = 0, so an index of 6 actually means Status, not Water.

The following code can be found at `BIN/BATTLE/BTLMOVE.EMI: 000144d8`.

```
; ; ; ; ; ; ; ; ; ;
; Intelligence    ;
; ; ; ; ; ; ; ; ; ;
801d37ac lui     $v0, 0x8012
801d37b0 lhu     $v0, -0x1f1c(v0) ; load caster's int
801d37b4 lui     $v1, 0xcccc
801d37b8 ori     $v1, 0xcccd 
801d37bc multu   $v0, $v1
801d37c0 mfhi    $a2, $hi
801d37c4 sw      $a2, 0x0020(fp)
801d37c8 lw      $a2, 0x0020(fp) 
801d37cc nop     
801d37d0 srl     $v0, $a2, 0x02 ; divide caster's int by 5
801d37d4 andi    $v1, $v0, 0xffff
801d37d8 addiu   $v0, $v1, 0x0032 ; add 50 to caster's int / 5. let this be alpha_1
801d37dc sw      $v0, 0x0014(fp) 
801d37e0 lw      $v0, 0x0014(fp)
801d37e4 nop     
801d37e8 slti    $v1, $v0, 0x0065
801d37ec bne     $v1, $r0, 0x801d37fc
801d37f0 nop     
	; If alpha_1 is greater than 100
	801d37f4 li      $v0, 0x0064 ; cap it to 100
	801d37f8 sw      $v0, 0x0014(fp) 
	
801d37fc lui     $v0, 0x8012
801d3800 lhu     $v0, -0x1eac(v0) ; load target's int
801d3804 lui     $v1, 0xcccc
801d3808 ori     $v1, 0xcccd
801d380c multu   $v0, $v1
801d3810 mfhi    $a2, $hi
801d3814 sw      $a2, 0x0020(fp)
801d3818 lw      $a2, 0x0020(fp)
801d381c nop     
801d3820 srl     $v0, $a2, 0x02 ; divide target's int by 5
801d3824 andi    $v1, $v0, 0xffff
801d3828 li      $v0, 0x004b 
801d382c subu    $v1, $v0, $v1 ; subtract target's int / 5 from 75. let this be alpha_2
801d3830 sw      $v1, 0x0018(fp) 
801d3834 lw      $v0, 0x0018(fp)
801d3838 nop     
801d383c slti    $v1, $v0, 0x0019 
801d3840 beq     $v1, $r0, 0x801d3850
801d3844 nop     
	; If alpha_2 is less than 25
	801d3848 li     $v0, 0x0019 ; cap it to 25
	801d384c sw      $v1, 0x0018(fp)
```
``
```
; ; ; ; ; ; ; ; ; ; ; ; ; ;
; Preparing resistances   ;
; ; ; ; ; ; ; ; ; ; ; ; ; ;
801d3850 lbu     $v0, 0x0010(fp) ; load index of attack's primary resistance
801d3854 lui     $at, 0x8012
801d3858 addu    $at, $v0
801d385c lbu     $v1, -0x1ea6(at) ; load primary resistance
801d3860 nop     
801d3864 sb      $v1, 0x001c(fp)
801d3868 lbu     $v0, 0x0010(fp) ; load index of attack's primary resistance
801d386c li      $v1, 0x0004
801d3870 bne     $v0, $v1, 0x801d38bc
801d3874 nop     
	; If the primary resistance is Holy
	801d3878 lb      $v0, 0x001c(fp) ; load primary resistnace
	801d387c nop     
	801d3880 bgtz    $v0, 0x801d3894
	801d3884 nop     
	
	; If the primary resistance is 0
	; The spell will succeed.

	; If the primary resistance is not 0
	801d3894 lb      $v0, 0x001c(fp) ; load primary resistance
	801d3898 nop     
	801d389c slti    $v1, $v0, 0x0005 
	801d38a0 bne     $v1, $r0, 0x801d38b4
	801d38a4 nop     

	; If the primary resistance is greater than or equal to 5
	; The spell will fail.

	; If the primary resistance is less than 5
	801d38b4 j       0x801d38f8 ; jump to 0x801d38f8, see below

; If the primary resistance is not Holy
801d38bc lb      $v0, 0x001c(fp) ; load primary resistance
801d38c0 nop     
801d38c4 bgtz    $v0, 0x801d38d8 
801d38c8 nop     

; If the primary resistance is 0
; The spell will succeed.

; If the primary resistance is greater than 0
801d38d8 lb      $v0, 0x001c(fp) ; load primary resistance
801d38dc nop     
801d38e0 slti    $v1, $v0, 0x0006 
801d38e4 bne     $v1, $r0, 0x801d38f8 
801d38e8 nop     

; If the primary resistance is greater than or equal to 6
; The spell will fail.

; If the primary resistance is less than 6
801d38f8 lbu     $v0, 0x0011(fp) ; load the index of the secondary resistance
801d38fc lui     $at, 0x8012 ; load the base address of the RNG table
801d3900 addu    $at, $v0 ; offset + base address
801d3904 lbu     $v1, -0x1eaa(at) ; load secondary resistance
801d3908 nop     
801d390c sb      $v1, 0x001d(fp) 
801d3910 lb      $v0, 0x001d(fp)
801d3914 nop     
801d3918 bgtz    $v0, 0x801d392c
801d391c nop     

; If the primary resistance is 0
; The spell will succeed.

; If the secondary resistance is greater than 0
801d392c lb      $v0, 0x001d(fp) ; load secondary resistance
801d3930 nop     
801d3934 slti    $v1, $v0, 0x0006 
801d3938 bne     $v1, $r0, 0x801d394c
801d393c nop     

; If the secondary resistance is greater than or equal to 6
; The spell will fail.

; The following code happens if the secondary resistance is less than 6
```

```
801d394c lw      $v0, 0x0014(fp) ; load alpha_1
801d3950 lw      $v1, 0x0018(fp) ; load alpha_2
801d3954 nop     
801d3958 mult    $v0, $v1 ; alpha_1 * alpha_2
801d395c mflo    $a2, $lo
801d3960 sw      $a2, 0x0024(fp)
801d3964 lw      $a2, 0x0024(fp)
801d3968 nop     
801d396c sw      $a2, 0x0014(fp)
801d3970 lw      $v0, 0x0014(fp)
801d3974 lui     $v1, 0x51eb
801d3978 ori     $v1, 0x851f
801d397c mult    $v0, $v1 
801d3980 mfhi    $a2, $hi
801d3984 sw      $a2, 0x0020(fp)
801d3988 lw      $a2, 0x0020(fp)
801d398c nop     
801d3990 sra     $v1, $a2, 0x05 ; alpha_1 * alpha2 / 100
801d3994 sra     $a0, $v0, 0x1f
801d3998 subu    $v0, $v1, $a0
801d399c sw      $v0, 0x0014(fp) 
801d39a0 lbu     $v0, 0x0010(fp) ; load index of primary resistane
801d39a4 li      $v1, 0x0004 
801d39a8 bne     $v0, $v1, 0x801d3a40
801d39ac nop     

; If the spell's primary resistance is Holy
801d39b0 lb      $v0, 0x001d(fp) ; load secondary resistance
801d39b4 nop     
801d39b8 move    $v1, $v0 
801d39bc sll     $v0, $v1, 0x01 ; calculate secondary resistance * 2
801d39c0 lui     $at, 0x801e ; load base address for the RNG table
801d39c4 addu    $at, $v0 ; base + offset
801d39c8 lh      $v1, 0x4fb8(at) ; load secondary multiplier
801d39cc lw      $v0, 0x0014(fp) ; load alpha1 * alpha2 / 100
801d39d0 nop     
801d39d4 mult    $v1, $v0 ; alpha1 * alpha2 / 100 * secondary multiplier
801d39d8 mflo    $a2, $lo
801d39dc sw      $a2, 0x0024(fp)
801d39e0 lb      $v0, 0x001c(fp) ; load primary resistance
801d39e4 nop     
801d39e8 move    $v1, $v0
801d39ec sll     $v0, $v1, 0x01 ; calculate primary resistance * 2
801d39f0 lui     $at, 0x801e ; load base address for the holy RNG table
801d39f4 addu    $at, $v0 ; base + offset
801d39f8 lh      $v1, 0x4fc8(at) ; load the primary multiplier
801d39fc lw      $a2, 0x0024(fp)
801d3a00 nop     
801d3a04 mult    $a2, $v1 ; alpha1 * alpha2 / 100 * secondary multiplier * primary multiplier
801d3a08 mflo    $v0, $lo
801d3a0c lui     $v1, 0x68db
801d3a10 ori     $v1, 0x8bad
801d3a14 mult    $v0, $v1 ; alpha1 * alpha2 / 100 * magic secondary * primary multiplier / 10000. let this be beta
801d3a18 mfhi    $a2, $hi
801d3a1c sw      $a2, 0x0020(fp)
801d3a20 lw      $a2, 0x0020(fp)
801d3a24 nop     
801d3a28 sra     $v1, $a2, 0x0c
801d3a2c sra     $v0, 0x1f
801d3a30 subu    $v1, $v0
801d3a34 sw      $v1, 0x0014(fp)
801d3a38 j       0x801d3ac8 ; call rand()
801d3a3c nop     

; If the spell's primary resistance is not Holy
801d3a40 lb      $v0, 0x001d(fp) ; load secondary resistance
801d3a44 nop     
801d3a48 move    $v1, $v0
801d3a4c sll     $v0, $v1, 0x01 ; calculate secondary resistance * 2
801d3a50 lui     $at, 0x801e ; load base address for the RNG table
801d3a54 addu    $at, $v0 ; base + offset
801d3a58 lh      $v1, 0x4fb8(at) ; load secondary multiplier
801d3a5c lw      $v0, 0x0014(fp) ; load alpha1 * alpha2 / 100
801d3a60 nop     
801d3a64 mult    $v1, $v0 ; alpha1 * alpha2 / 100 * secondary multiplier
801d3a68 mflo    $a2, $lo 
801d3a6c sw      $a2, 0x0024(fp)
801d3a70 lb      $v0, 0x001c(fp) ; load primary resistance
801d3a74 nop     
801d3a78 move    $v1, $v0
801d3a7c sll     $v0, $v1, 0x01 ; calculate primary resistance * 2
801d3a80 lui     $at, 0x801e ; load base address for the RNG table
801d3a84 addu    $at, $v0 ; base + offset
801d3a88 lh      $v1, 0x4fb8(at) ; load primary multiplier
801d3a8c lw      $a2, 0x0024(fp) ; load alpha1 * alpha2 / 100 * secondary multiplier
801d3a90 nop     
801d3a94 mult    $a2, $v1 ; alpha1 * alpha2 / 100 * secondary multiplier * primary multiplier
801d3a98 mflo    $v0, $lo
801d3a9c lui     $v1, 0x68db
801d3aa0 ori     $v1, 0x8bad
801d3aa4 mult    $v0, $v1 ; alpha1 * alpha2 / 100 * magic secondary * primary multiplier / 10000. let this be beta
801d3aa8 mfhi    $a2, $hi
801d3aac sw      $a2, 0x0020(fp)
801d3ab0 lw      $a2, 0x0020(fp)
801d3ab4 nop     
801d3ab8 sra     $v1, $a2, 0x0c 
801d3abc sra     $v0, 0x1f
801d3ac0 subu    $v1, $v0
801d3ac4 sw      $v1, 0x0014(fp) 
801d3ac8 jal     0x8016f384 ; call rand()
801d3acc nop     
...
801d3ad8 mult    $v0, $v1 
801d3adc mfhi    $a2, $hi
801d3ae0 sw      $a2, 0x0020(fp)
801d3ae4 lw      $a2, 0x0020(fp)
801d3ae8 nop     
801d3aec sra     $v1, $a2, 0x05 ; divide rand() by 100
801d3af0 sra     $a0, $v0, 0x1f
801d3af4 subu    $v1, $a0
801d3af8 move    $a1, $v1
801d3afc sll     $a0, $a1, 0x01 ; rand() / 100 * 2
801d3b00 addu    $a0, $v1 ; rand() / 100 * 3
801d3b04 sll     $a1, $a0, 0x03 ; rand() / 100 * 24
801d3b08 addu    $a1, $v1 ; rand() / 100 * 25
801d3b0c sll     $v1, $a1, 0x02 // rand() / 100 * 100
801d3b10 subu    $v0, $v1 ; get a random number between 0 and 99
801d3b14 lw      $v1, 0x0014(fp) // load beta
801d3b18 nop     
801d3b1c subu    $v0, $v1 ; random(0,99) - beta
801d3b20 bgez    $v0, 0x801d3b34 ; if negative, the spell is sucessful
```