Healing is completely deterministic and does not rely on any random-number generation.
## Field
$$
h = \left\lfloor\frac{10P\cdot INT_A}{100}\right\rfloor + 10P
$$
```
801ab228 lbu     $v0, 0x0003(v0) ; load spell power
801ab22c andi    $a0, 0x00ff
801ab230 sll     $a2, $v0, 0x02 ; multiply spell power by 4
801ab234 addu    $a2, $v0 ; multiply spell power by 5
801ab238 sll     $v0, $a0, 0x02 
801ab23c addu    $v0, $a0 
801ab240 sll     $v0, 0x02 
801ab244 subu    $v0, $a0 
801ab248 sll     $v0, 0x03
801ab24c addu    $v0, $a3
801ab250 lhu     $v0, 0x0048(v0) ; load caster's int
801ab254 sll     $a2, 0x01 ; multiply spell power by 10
801ab258 mult    $a2, $v0 ; multiply caster's int by spell power * 10
801ab25c mflo    $v0, $lo
801ab260 lui     $v1, 0x51eb
801ab264 ori     $v1, 0x851f
801ab268 mult    $v0, $v1
801ab26c andi    $a1, 0x00ff
801ab270 sll     $a0, $a1, 0x02
801ab274 addu    $a0, $a1
801ab278 sll     $a0, 0x02
801ab27c subu    $a0, $a1
801ab280 sll     $a0, 0x03
801ab284 addu    $a0, $a3
801ab288 sra     $v0, 0x1f
801ab28c mfhi    $v1, $hi
801ab290 sra     $v1, 0x05 ; divide caster's int by spell power * 10 by 100
801ab294 subu    $v1, $v0
801ab298 jal     0x801ab4ac
801ab29c addu    $a1, $a2, $v1 ; add spell power * 10 to caster's int by spell power * 10 / 100
801ab4ac addiu   $sp, -0x0018
801ab4b0 sw      $ra, 0x0014(sp)
801ab4b4 sw      $s0, 0x0010(sp)
801ab4b8 lw      $v1, 0x0014(a0) ; load target's HP
801ab4bc lw      $v0, 0x0038(a0)
801ab4c0 nop     
801ab4c4 bne     $v1, $v0, 0x801ab4d4
801ab4c8 li      $s0, 0x0001
801ab4d4 addu    $v0, $v1, $a1 ; add the healing amount to the target's HP
801ab4d8 jal     0x801ab0cc
801ab4dc sw      $v0, 0x0014(a0) ; store new HP
```
Python implementation
```python
def heal_battle(int_a, p):
	retrun (10 * int_a * p) // 100 + 10 * p
```
## Battle
$$
h=\left\lfloor\frac{\delta F}{100}\right\rfloor
$$
$$
\alpha=10(100+20\rho_\mathrm{holy})P
$$
$$
\beta = \left\lfloor\frac{(100 + INT_{A})\alpha}{100}\right\rfloor
$$
$$
\gamma = \left\lfloor\frac{R'_\mathrm{magic}\beta}{100}\right\rfloor
$$
$$
\delta = -\left\lfloor \frac{R'_\mathrm{holy}\gamma}{10000}\right\rfloor
$$

* $\rho_\mathrm{holy}$ = [[In-a-Row Combo]] for holy spells
* $P$ = Spell power
* $R'_\mathrm{magic}$ = Healing factor based on the target's magic resistance
* $R'_\mathrm{holy}$ = Healing factor based on the target's holy resistance
* $F$ = The spell's sequela multiplier

The following code can be found at `BIN/BATTLE/BTLMOVE.EMI: 00011d2c`
```
; ; ; ; ; ; ; ; ;
; Spell Power   ;
; ; ; ; ; ; ; ; ;
801d9d2c lbu     $v1, 0x0002(s1) ; load spell power
801d9d30 li      $v0, 0x00ff
801d9d34 bne     $v1, $v0, 0x801d9d60
801d9d38 lui     $s0, 0x8012

; If the spell is not a max-healing spell
801d9d60 lbu     $v0, 0x0002(s1) ; load spell power
801d9d64 nop     
801d9d68 sll     $a0, $v0, 0x02 ; multiply spell power by 4
801d9d6c addu    $a0, $v0 ; multiply spell power by 5
801d9d70 jal     0x801d4620
801d9d74 sll     $a0, 0x01 ; multiply spell power by 10
...
801d8040 sw      $s0, 0x0010(sp) ; store 10 * spell power
```

```
; ; ; ; ; ; ; ; ; ; ;
; In-a-row combo    ;
; ; ; ; ; ; ; ; ; ; ;
801d81dc lb      $v1, 0x0054(v0) ; load the in-a-row combo for holy spells
801d81e0 lbu     $a2, 0x0054(v0) ; load the in-a-row combo for holy spells
801d81e4 beq     $v1, $r0, 0x801d81f4
801d81e8 addiu   $v0, $a2, -0x0001

; If the in-a-row count is zero
801d81f4 move    $v0, $r0 ; set the in-a-row combo
...
801d4638 sll     $v1, $v0, 0x02 ; multiply the in-a-row combo by 4
801d463c addu    $v1, $v0 ; multiply the in-a-row combo by 5
801d4640 sll     $v1, 0x02 ; multiply the in-a-row combo by 20
801d4644 addiu   $v1, 0x0064 ; add 100 to 20 * in-a-row combo. 
```

```
801d4648 mult    $s0, $v1 ; multiply 10 * spell power by 100 + in-a-row combo. let this be alpha
801d4650 lhu     $v0, -0x1f1c(v0) ; load caster's int
801d4654 mflo    $s0, $lo
801d4658 addiu   $v0, 0x0064 ; add 100 to the caster's int
801d465c nop     
801d4660 mult    $s0, $v0 ; multiply 100 + caster's int by alpha
801d4664 mflo    $s0, $lo
801d4668 lui     $a0, 0x51eb
801d466c ori     $a0, 0x851f
801d4670 mult    $s0, $a0
801d4674 sra     $v0, $s0, 0x1f
801d4678 mfhi    $v1, $hi 
801d467c sra     $v1, 0x05 ; divide (100 + int) * alpha by 100. let this be beta
801d4680 subu    $s0, $v1, $v0
801d4684 lui     $v0, 0x8012
801d4688 addiu   $a1, $v0, -0x1ed0
801d468c lbu     $v0, 0x0028(a1) ; load the target's magic resistance
801d4690 li      $a2, 0x0001
801d4694 bne     $v0, $a2, 0x801d46b8
801d4698 lui     $v0, 0x801e

; If the target's magic resistance is not equal to 1
801d46b8 lbu     $v1, 0x0028(a1) ; load the target's magic resistance
801d46bc addiu   $v0, 0x5140 ; load the base address of the magic resistance healing factor table
801d46c0 addu    $v1, $v0 ; offset + base address 
801d46c4 lbu     $v0, 0x0000(v1) ; load the magic resistance's healing factor
801d46c8 nop    
801d46cc mult    $s0, $v0 ; multiply beta by the magic resistance's healing factor
801d46d0 mflo    $v0, $lo
801d46d4 nop     
801d46d8 nop     
801d46dc mult    $v0, $a0 
801d46e0 sra     $v0, 0x1f
801d46e4 mfhi    $v1, $hi
801d46e8 sra     $a0, $v1, 0x05  ; divide beta * healing factor by 100
801d46ec lbu     $v1, 0x002e(a1) ; load target's holy resistance
801d46f0 nop     
801d46f4 bne     $v1, $a2, 0x801d4714
801d46f8 subu    $s0, $a0, $v0

; If the target's holy resistance is not equal to 1
801d4714 lui     $v1, 0x801e
801d4718 lbu     $v0, 0x002e(a1)  ; load the target's holy resistance
801d471c addiu   $v1, 0x5148 ; load the base address of the holy resistance healing factor table
801d4720 sll     $v0, 0x01 ; multiply the holy resistance by 2
801d4724 addu    $v0, $v1 ; offset + base address
801d4728 lh      $v0, 0x0000(v0) ; load the holy resistance's healing factor
801d472c nop     
801d4730 mult    $s0, $v0 ; multiply beta * healing factor / 100 by the holy resistance's healing factor
801d4734 mflo    $v0, $lo
801d4738 lui     $v1, 0x68db
801d473c ori     $v1, 0x8bad
801d4740 mult    $v0, $v1 
801d4744 lw      $ra, 0x0014(sp)
801d4748 sra     $v0, 0x1f
801d474c mfhi    $v1, $hi
801d4750 sra     $v1, 0x0c ; divide  beta * healing factor / 100 * holy resistance's healing factor by 10000
801d4754 subu    $s0, $v1, $v0
801d4758 subu    $v0, $r0, $s0 ; make the value negative. let this be delta
...
801d9d84 sw      $v0, 0x000c(v1) ; store delta
...
801d9de8 lbu     $v0, 0x0000(s1) ; load the spell's sequela multiplier
801d9df4 mult    $v1, $v0 ; multiply delta by the multiplier
801d9df8 mflo    $v1, $lo
801d9dfc lui     $v0, 0x51eb
801d9e00 ori     $v0, 0x851f
801d9e04 mult    $v1, $v0
801d9e08 sra     $v1, 0x1f
801d9e0c mfhi    $t1, $hi
801d9e10 sra     $v0, $t1, 0x05 ; divide delta by the 100
801d9e14 subu    $v0, $v1
801d9e18 sw      $v0, 0x000c(a0) ; store the final amount of HP healed
```
Python implementation:
```python
def heal_battle(int_a, p, iar, r_magic, r_holy, seq):
	magic_tbl = [0, 50, 100, 100, 100, 100, 100, 100]
	holy_tbl = [-200, -150, 0, 25, 50, 100, 200, 300]
	alpha = 10 * (100 + iar) * p
	beta = ((100 + int_a) * alpha) // 100
	gamma = (magic_tbl[r_magic] * beta) // 100
	return (holy_tbl[r_holy] * gamma) // 10000
```