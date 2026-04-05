| ID           | Equipped By | Element | Weight | Power | Hits | Shield Damage |
| ------------ | ----------- | ------- | ------ | ----- | ---- | ------------- |
| `0x17`<br>23 | Scias       | None    | 0      | 2     | 1    | 1             |
Chopsticks causes instant death on Fly-type enemies
```
801d9938 9043011c: lbu    $v1(0000000e), 0x011c(v0)([801c7e1c] = 17) ; load the weapon's ID
801d993c 24020017: li     $v0(801c7d00), 0x0017 ; load Chopsticks' ID
801d9940 14620021: bne    $v1(00000017), $v0(00000017), 0x801d99c8
801d9944 3c05801c: lui    $a1(801c7018), 0x801c
; if the current weapon is Chopsticks
801d9948 8e02000c: lw     $v0(00000017), 0x000c(s0)([8011e13c] = 801c6ec0)
801d994c 00000000: nop    
Breakpoint condition met! Type:Always reading:7 condVal:0
Breakpoint triggered: PC=0x801d9950 - Cause: 801c6ec2::Read::1 (GUI) 
801d9950 90430002: lbu    $v1(00000017), 0x0002(v0)([801c6ec2] = 07) ; load enemy's type
801d9954 24020007: li     $v0(801c6ec0), 0x0007 ; load the Fly type's ID
801d9958 1462001c: bne    $v1(00000007), $v0(00000007), 0x801d99cc
801d995c 24a579b8: addiu  $a1(801c0000), 0x79b8
; if the enemy's type is Fly, causes instant death
... 
```
The code can be found at `BIN/BATTLE/BTLMOVE.EMI: 00011938`