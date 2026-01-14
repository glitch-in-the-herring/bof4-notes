Critical hits are melee/ranged hits that deal more damage than normal. The extra hit is computed by the following formula:
$$
d' = d + 10\left(\left\lfloor\frac{ATK_A}{4}\right\rfloor + L_A\right)
$$
The code can be found at the following locations:
```
BIN/BATTLE/BTLRET.EMI: 00011f08
BIN/SYSTEM/FLD_MAIN.EMI: 00027708
BIN/WORLD/D141BTL.EMI: 00011f08
BIN/WORLD/D142BTL.EMI: 00011f08
BIN/WORLD/D152BTL.EMI: 00011f08
BIN/WORLD/E077BTL.EMI: 00011f08
```

```
801d9708 lhu     $v1, 0x001e(v1) ; load attacker's ATK
801d970c lhu     $v0, 0x00a6(v0) ; load attacker's level
801d9710 srl     $v1, 0x02 ; divide attacker's ATK by 4
801d9714 addu    $v1, $v0 ; ATK / 4 + level
801d9718 sll     $v0, $v1, 0x02 ; (ATK / 4 + level) * 4
801d971c addu    $v0, $v1 ; (ATK / 4 + level) * 5
801d9720 sll     $v0, 0x01 ; (ATK / 4 + level) * 10
801d9724 j       0x801d9750
801d9728 addu    $v0, $a0, $v0 ; add extra damage to the previous damage
801d9750 sw      $v0, 0x000c(a1) ; store damage
```
The roll is calculated by the following formula:
$$
r = \mathrm{random}(0,99)-\mathcal{C}
$$
$$
\begin{cases}
\mathrm{success} & r < 0\\
\mathrm{fail}&r\geq0
\end{cases}
$$
* $\mathcal{C}$ is the attacker's critical rate
In other words, the probability of landing a critical hit is attacker's critical rate divided by 100.
The code can be found at `BIN/BATTLE/BTLMOVE.EMI: 00017638`
```
801df638 jal     0x8016f384 ; call rand()
801df648 mult    $v0, $v1 ; rand() / 100
801df64c sra     $v1, $v0, 0x1f
801df650 mfhi    $a2, $hi
801df654 sra     $a0, $a2, 0x05
801df658 subu    $a0, $v1
801df65c sll     $v1, $a0, 0x01 ; rand / 100 * 2
801df660 addu    $v1, $a0 ; rand / 100 * 3
801df664 sll     $v1, 0x03 ; rand / 100 * 24
801df668 addu    $v1, $a0 ; rand / 100 * 25
801df66c sll     $v1, 0x02 ; rand / 100 * 100
801df670 lui     $a0, 0x8012
801df674 addiu   $a1, $a0, -0x1f40
801df678 lbu     $a0, 0x0034(a1) ; load the attacker's critical rate
801df67c subu    $v0, $v1 ; random(0,99)
801df680 subu    $v0, $a0 ; random(0,99) - critical rate
801df684 bgez    $v0, 0x801df700 

; If the critical attack lands
...
801df6a0 ori     $vi, 0x0004 ; set the attacker's critical bit
```