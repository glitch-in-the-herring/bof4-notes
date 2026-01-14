## Probability Table
The probability table is shared for both steal and drop. It can be found at:
* `0x801e526c` in the RAM
* `BIN/BATTLE/BTLMOVE.EMI: 0001d26c`

| Value | $P$ |
| ----- | --- |
| 0     | 0   |
| 1     | 2   |
| 2     | 4   |
| 3     | 16  |
| 4     | 32  |
| 5     | 64  |
| 6     | 128 |
| 7     | 256 |
## Steal
### Steal Roll
$$
\Delta_{AGL} =  AGL_{A} - AGL_{D}
$$
$$F_{AGL}=\begin{cases}
0 &  \Delta_{AGL} < -30 \\
\left\lfloor\frac{\Delta_{AGL} + 40}{10}\right\rfloor & -30 < \Delta_{AGL}  < 41\\
8 & \Delta_{AGL} > 41
\end{cases}$$
$\alpha$ values:

| $F_{AGL}$ | $\alpha$ |
| --------- | -------- |
| 0         | 5        |
| 1         | 6        |
| 2         | 7        |
| 3         | 8        |
| 4         | 8        |
| 5         | 9        |
| 6         | 10       |
| 7         | 11       |
| 8         | 12       |
Let $F_C$ be the combo factor. This value is equal to the "element in a row count" - 1 (the visually smaller number in the combo HUD) when there is a combo. If the spell is not part of a combo, then it is 0.
$\beta$ values:

| $F_{C}$ | $\beta$ |
| ------- | ------- |
| 0       | 0       |
| 1       | 2       |
| 2       | 4       |

$$
r = \mathrm{random}(0, 2047) - (\alpha+\beta)P
$$
$$
\begin{cases}
\mathrm{success} & r < 0\\
\mathrm{fail} & r \geq 0
\end{cases}
$$
### Code
Can be found at `BIN/BATTLE/BTLMOVE.EMI: 00013c38`
```
; ; ; ; ; ; ; ; ; ; ;
; Calculate F_AGL   ;
; ; ; ; ; ; ; ; ; ; ;

801dbc38 lhu     $v1, -0x1f1e(v0) ; load attacker's AGL
801dbc3c lhu     $v0, 0x0022(a1) ; load defender's AGL
801dbc40 nop     
801dbc44 subu    $a0, $v1, $v0 ; calculate attacker's AGL - defender's AGL
801dbc48 slti    $v0, $a0, -0x001e
801dbc4c bne     $v0, $r0, 0x801dbc84
; If the difference is less than -30:
	801dbc50 move    $s3, $r0 ; Set F_AGL to 0

; If the difference is more than or equal to -30:
	801dbc54 slti    $v0, $a0, 0x0029
    801dbc58 bne     $v0, $r0, 0x801dbc68
	    ; If the difference is more than 41
	    801dbc60 j       0x801dbc84
		801dbc64 li      $s3, 0x0008 ; Set F_AGL to 8

		; If the difference is less than 41
	    801dbc5c lui     $v1, 0x6666
	    801dbc68 ori     $v1, 0x6667
	    801dbc6c addiu   $v0, $a0, 0x0028 ; Add 40 to the difference
	    801dbc70 mult    $v0, $v1
	    801dbc74 sra     $v0, 0x1f
	    801dbc78 mfhi    $a3, $hi 
	    801dbc7c sra     $v1, $a3, 0x02 ; Divide (40 + Delta_AGL) by 100, rounded down
	    801dbc80 subu    $s3, $v1, $v0 ; Set F_AGL to the value above.

```

```
; ; ; ; ; ; ; ; ; ;
; Calculate F_C   ;
; ; ; ; ; ; ; ; ; ;
801d81dc lb      $v1, 0x0054(v0) ; load the "in-a-row" combo count to $v1
801d81e0 lbu     $a2, 0x0054(v0) ; load the "in-a-row" combo count to $a2
801d81e4 beq     $v1, $r0, 0x801d81f4 
; If the "in-a-row" combo count is not 0
	801d81e8 addiu   $v0, $a2, -0x0001 ; set F_C to "in-a-row" combo count - 1

; If the "in-a-row" combo count is 0
	801d81f4 move    $v0, $r0 ; set F_C to 0
```

```
; ; ; ; ; ; ; ; ; ; ; ; ; ; ; ; ; ;
; Putting it all together         ;
; ; ; ; ; ; ; ; ; ; ; ; ; ; ; ; ; ;
801dbcbc jal     0x8016f384 ; call the random number function
...
801dbcc8 move    $s1, $v0 ; move the random number to $s1
...
801dbcd4 move    $a0, $v0
...
801d81fc lw      $s0, 0x0010(sp) ; load the steal rate
801dbccc move    $a2, $s1 ; move the random number to $a2
801dbcd0 bgez    $s1, 0x801dbcdc
801dbcd4 move    $a0, $v0
; If the random number is negative
	801dbcd8 addiu   $a2, $s1, 0x07ff ; make it positive

801dbcdc lui     $v0, 0x801e
801dbce0 addiu   $v0, 0x526c ; the base address of P values is 0x801e526c
801dbce4 andi    $a1, s0, 0x00ff
801dbce8 sll     $a1, 0x01 ; multiply the steal rate by 2 to make the offset
801dbcec addu    $a1, $v0 ; add the offset to the base address
801dbcf0 lui     $v0, 0x801e
801dbcf4 addiu   $v0, 0x5288 ; the base address of beta values is 0x801e5288
801dbcf8 andi    $a0, 0x00ff 
801dbcfc addu    $a0, $v0 ; add F_C the offset to the base address
801dbd00 lui     $v0, 0x801e
801dbd04 addiu   $v0, 0x527c ; the base address of alpha values is 0x801e527c
801dbd08 andi    $v1, $s3, 0x00ff
801dbd0c addu    $v1, $v0 ; add F_AGL as the offset to the base address
801dbd10 lbu     $v0, 0x0000(a0) ; load beta
801dbd14 lbu     $v1, 0x0000(v1) ; load alpha
801dbd18 lhu     $a0, 0x0000(a1) ; load P
801dbd1c addu    $v0, $v1 ; add alpha and beta
801dbd20 mult    $a0, $v0 ; multiply P by (alpha + beta)
801dbd24 sra     $v0, $a2, 0x0b ; divide the random number by 2048
801dbd28 sll     $v0, 0x0b ; multiply the result by 2048, rounding the random number to the smallest multiple of 2048
801dbd2c subu    $v0, $s1, $v0 ; limits the random number to 0 - 2047
801dbd30 mflo    $a3, $lo 
801dbd34 subu    $v0, $a3 ; calculate \mathrm{random}(0,2047) - (alpha+beta)*P
801dbd38 bgez    $v0, 0x801dbdb4 ; jump if fails
```
## Drop
### Drop Roll
$$
r = \mathrm{random}(0,255) - P
$$
This is a straightforward roll and the probabilities can be easily computed:

| Value | $p$      |
| ----- | -------- |
| 0     | 0%       |
| 1     | 0.78125% |
| 2     | 1.5625%  |
| 3     | 6.25%    |
| 4     | 12.5%    |
| 5     | 25%      |
| 6     | 50%      |
| 7     | 100%     |
