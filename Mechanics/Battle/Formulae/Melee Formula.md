
$$
d = \left\lfloor\frac{R_w\delta}{10000}\right\rfloor
$$
$$
\Delta PWR = \begin{cases}
PWR_{A} - DEF_{D} + \mathrm{random}(0,1)  &  PWR_{A}- DEF_{D} > 0\\
0 + \mathrm{random}(0,1) & PWR_{A} - DEF_{D} \leq 0
\end{cases}
$$

$$
\alpha = 100 - \left\lfloor\frac{100\Delta PWR}{5000}\right\rfloor
$$
$$
\beta = \begin{cases}
\left\lfloor\frac{100\Delta PWR \alpha}{100}\right\rfloor  & \alpha \geq 80\\[1.5em]
\left\lfloor\frac{8000\Delta PWR}{100}\right\rfloor& \alpha < 80
\end{cases}
$$
$$
 \gamma = \left\lfloor\frac{\beta \mathrm{random}(900,1100)}{100}\right\rfloor
$$
$$
\delta = \left\lfloor\frac{R_e\gamma}{100}\right\rfloor
$$
* $R_e$ is the target's elemental resistance to the weapon's element
* $R_w$ is the target's melee/ranged resistance
## Code
The following code can be found at `BIN/BATTLE/BTLMOVE.EMI: 0000bef8`
```
801d3ef8 lhu     $v1, 0x001e(s0) ; load attacker's PWR
801d3efc lhu     $v0, 0x0020(a0) ; load target's DEF
801d3f00 nop     
801d3f04 subu    $s1, $v1, $v0 ; Subtract the attacker's ATK from the target's DEF
801d3f08 bgez    $s1, 0x801d3f14
801d3f0c nop    

; If the result of the subtraction is greater than zero
801d3f14 jal     0x8016f384 ; call rand()
801d3f18 nop    
...
801d3f1c andi    $v0, 0x0001 ; choose randomly between 0 and 1
801d3f20 addu    $v0, $s1, $v0 ; add the random number to the subtraction result. Call this Delta
801d3f24 sll     $v1, $v0, 0x01 ; multiply Delta by 2
801d3f28 addu    $v1, $v0 ; multiply Delta by 3
801d3f2c sll     $v1, 0x03 ; multiply Delta by 24
801d3f30 addu    $v1, $v0 ; multiply Delta by 25
801d3f34 j       0x801d40a4
801d3f38 sll     $s1, $v1, 0x02 ; multiply Delta by 100. This will be quite common, so let this be 100Delta
801d40a4 lui     $v0, 0x68db
801d40a8 ori     $v0, 0x8bad
801d40ac mult    $s1, $v0
801d40b0 sra     $v1, $s1, 0x1f
801d40b4 mfhi    $t0, $hi
801d40b8 sra     $v0, $t0, 0x0b ; divide 100Delta by 5000 
801d40bc subu    $v0, $v1
801d40c0 li      $v1, 0x0064
801d40c4 subu    $v1, $v0 ; subtract  100Delta / 5000 from 100, let this be alpha
801d40c8 slti    $v0, $v1, 0x0050
801d40cc bne     $v0, $r0, 0x801d40e4

; If alpha is greater than or equal to 80
801d40d0 sll     $v0, $s1, 0x02 ; multiply 100Delta by 4
801d40d4 mult    $s1, $v1 ; multiply 100Delta by alpha
801d40d8 mflo    $v0, $lo
801d40dc j       0x801d40f0
801d40e0 move    $s1, $v0 
801d40f0 lui     $s0, 0x51eb
801d40f4 ori     $s0, 0x851f
801d40f8 mult    $s1, $s0
801d40fc sra     $v0, $s1, 0x1f
801d4100 mfhi    $v1, $hi
801d4104 sra     $v1, 0x05 ; divide 100Delta * alpha by 100. Let this be beta.
801d4108 jal     0x8016f384 ; call rand()
801d410c subu    $s1, $v1, $v0
...
801d4110 lui     $v1, 0x028c
801d4114 ori     $v1, 0x1979
801d4118 mult    $v0, $v1 ; multiply rand() by 2/201
801d411c mfhi    $v1, $hi
801d4120 sra     $a0, $v1, 0x01 ; divide rand() * 2/201 by 2
801d4124 sra     $v1, $v0, 0x1f 
801d4128 subu    $a0, $v1
801d412c sll     $v1, $a0, 0x01  ; multiply rand() * 2/201 / 2 by 2
801d4130 addu    $v1, $a0 ; multiply rand() * 2/201 / 2 by 3
801d4134 sll     $v1, 0x03 ; multiply rand() * 2/201 / 2 by 24
801d4138 addu    $v1, $a0 ; multiply rand() * 2/201 / 2 by 25
801d413c sll     $v1, 0x03 ; multiply rand() * 2/201 / 2 by 200
801d4140 addu    $v1, $a0 ; multiply rand() * 2/201 / 2 by 201
801d4144 subu    $v0, $v1 ; get a random number between 0 and 200
801d4148 addiu   $v0, 0x0384 ; add 900 to the random number, meaning that the random number range is now between 900 and 1100
801d414c mult    $s1, $v0 ; multiply beta by random(900,1100)
801d4150 mflo    $s1, $lo
801d4154 nop    
801d4158 nop    
801d415c mult    $s1, $s0
801d4160 andi    $a0, $s2, 0x00ff
801d4164 sra     $v0, $s1, 0x1f
801d4168 mfhi    $v1, $hi
801d416c sra     $v1, 0x05 ; divide beta * random(900,110) by 100. let this be gamma
801d4170 subu    $s1, $v1, $v0
801d4174 li      $v0, 0x00ff
801d4178 bne     $a0, $v0, 0x801d418c
801d417c nop    
801d4180 jal     0x801d4e10
801d4184 nop    
801d4e10 lui     $a2, 0x8012
801d4e14 addiu   $a0, $a2, -0x1f40
801d4e18 lbu     $v1, 0x0001(a0)
801d4e1c li      $v0, 0x0004
801d4e20 beq     $v1, $v0, 0x801d4eb8
801d4e24 slti    $v0, $v1, 0x0005
801d4e28 beq     $v0, $r0, 0x801d4e40
801d4e2c li      $v0, 0x0001
801d4e30 beq     $v1, $v0, 0x801d4e54
801d4e34 move    $v0, $r0
801d4e54 lbu     $v0, -0x1f40(a2)
801d4e58 nop    
801d4e5c sltiu   $v0, 0x0006
801d4e60 beq     $v0, $r0, 0x801d4eb0
801d4e64 lui     $a1, 0x801a
801d4e68 lui     $a0, 0x801c
801d4e6c lbu     $v0, -0x1f40(a2)
801d4e70 addiu   $a0, 0x79b8
801d4e74 sll     $v1, $v0, 0x03
801d4e78 subu    $v1, $v0
801d4e7c sll     $v0, $v1, 0x04
801d4e80 subu    $v0, $v1
801d4e84 sll     $v0, 0x02
801d4e88 addu    $v0, $a0
801d4e8c lbu     $v1, 0x011c(v0)
801d4e90 addiu   $a1, -0x5eac
801d4e94 sll     $v0, $v1, 0x03
801d4e98 subu    $v0, $v1
801d4e9c sll     $v0, 0x01
801d4ea0 addu    $v0, $a1
801d4ea4 lbu     $v0, 0x0005(v0) ; load the element of the weapon
...
; the result is delta
801d41d4 lbu     $v0, 0x0026(v0) ; load the target's physical resistance
801d41d8 addiu   $v1, 0x5120
801d41dc sll     $v0, 0x01
801d41e0 addu    $v0, $v1
801d41e4 lh      $v0, 0x0000(v0) ; load the physical resistance multiplier
801d41e8 nop     
801d41ec mult    $s1, $v0 ; multiply delta by the physical resistance multiplier
801d41f0 mflo    $s1, $lo
801d41f4 jal     0x801d4c7c
801d41f8 nop     
801d4c7c lui     $a2, 0x8012
801d4c80 addiu   $a0, $a2, -0x1f40
801d4c84 lbu     $v1, 0x0001(a0)
801d4c88 li      $v0, 0x0004
801d4c8c beq     $v1, $v0, 0x801d4d84
801d4c90 slti    $v0, $v1, 0x0005
801d4c94 beq     $v0, $r0, 0x801d4cac
801d4c98 li      $v0, 0x0001
801d4c9c beq     $v1, $v0, 0x801d4cc0
801d4ca0 move    $v0, $r0
801d4cc0 lbu     $v0, -0x1f40(a2)
801d4cc4 nop     
801d4cc8 sltiu   $v0, 0x0006
801d4ccc beq     $v0, $r0, 0x801d4d50
801d4cd0 nop     
801d4cd4 lw      $v0, 0x000c(a0)
801d4cd8 nop     
801d4cdc lhu     $v0, 0x00ae(v0)
801d4ce0 nop     
801d4ce4 andi    $v0, 0x0080
801d4ce8 beq     $v0, $r0, 0x801d4cf8
801d4cec lui     $a1, 0x801a
801d4cf8 lui     $a0, 0x801c
801d4cfc lbu     $v0, -0x1f40(a2)
801d4d00 addiu   $a0, 0x79b8
801d4d04 sll     $v1, $v0, 0x03
801d4d08 subu    $v1, $v0
801d4d0c sll     $v0, $v1, 0x04
801d4d10 subu    $v0, $v1
801d4d14 sll     $v0, 0x02
801d4d18 addu    $v0, $a0
801d4d1c lbu     $v1, 0x011c(v0)
801d4d20 addiu   $a1, -0x5eac
801d4d24 sll     $v0, $v1, 0x03
801d4d28 subu    $v0, $v1
801d4d2c sll     $v0, 0x01
801d4d30 addu    $v0, $a1
801d4d34 lhu     $v0, 0x0000(v0)
801d4d38 nop     
801d4d3c andi    $v0, 0x0800
801d4d40 beq     $v0, $r0, 0x801d4e08
801d4d44 move    $v0, $r0
801d4e08 jr      $ra
801d4e0c nop     
801d41fc andi    $v0, 0x00ff
801d4200 addu    $v0, $s0
801d4204 lbu     $v0, 0x0026(v0)
801d4208 nop     
801d420c addu    $v0, $s0
801d4210 lbu     $v1, 0x0026(v0)
801d4214 li      $v0, 0x0001
801d4218 bne     $v1, $v0, 0x801d423c
801d421c lui     $v0, 0x68db
801d423c ori     $v0, 0x8bad
801d4240 mult    $s1, $v0 ; divide delta by 10000
801d4244 sra     $v0, $s1, 0x1f
801d4248 lw      $ra, 0x001c(sp)
801d424c lw      $s2, 0x0018(sp)
801d4250 lw      $s1, 0x0014(sp)
801d4254 lw      $s0, 0x0010(sp)
801d4258 mfhi    $t0, $hi
801d425c sra     $v1, $t0, 0x0c
801d4260 subu    $v0, $v1, $v0 ; damage
```