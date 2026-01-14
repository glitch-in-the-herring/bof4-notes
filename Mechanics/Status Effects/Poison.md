The Poison status causes the afflicted character to lose HP over time.
## Field
While walking, the character loses 1 HP for every 5 steps
```
801da2a4 li      $a0, 0x0001 ; load 1 to $a0
...
801d74e4 lw      $v1, 0x0014(a1) ; load the character's current HP
801d74e8 andi    $v0, $a0, 0xffff
801d74ec sltu    $v0, $v1 
801d74f0 bne     $v0, $r0, 0x801d7504
801d74f4 nop

; If the character's HP is less than or equal to 1
801d74f8 lhu     $v0, 0x0014(a1) ; load the character's current HP
801d74fc j       0x801d7508
801d7500 addiu   $v0, -0x0001 ; set the subtractor to 0

; If the character's HP is more than 1
801d7504 move    $v0, $a0
801d7508 andi    $a0, $v0, 0xffff
801d750c lw      $v1, 0x0014(a1) ; load the character's current HP
801d7510 lw      $v0, 0x0038(a1) ; load the character's max HP
801d7514 subu    $v1, $a0 ; subtract the character's current hp by 1
801d7518 srl     $v0, 0x02 ; divide the character's max HP by 4
801d751c sltu    $v0, $v1
801d7520 bne     $v0, $r0, 0x801d7538
801d7524 sw      $v1, 0x0014(a1) ; store the character's new HP

; If the character's HP is less than a quarter
801d7528 lhu     $v0, 0x0012(a1) ; load the character's status bytes
801d752c nop     
801d7530 ori     $v0, 0x4000 ; set a status
801d7534 sh      $v0, 0x0012(a1) ; store the character's status
```
The code can be found at:
```
801da2a4:
BIN/BATTLE/BTLRET.EMI: 00012aa4
BIN/SYSTEM/FLD_MAIN.EMI: 000282a4
BIN/WORLD/D141BTL.EMI: 00012aa4
BIN/WORLD/D142BTL.EMI: 00012aa4
BIN/WORLD/D152BTL.EMI: 00012aa4
BIN/WORLD/E077BTL.EMI: 00012aa4
```

```
801d74e4:
BIN/BATTLE/BTLRET.EMI: 0000fce4
BIN/SYSTEM/FLD_MAIN.EMI: 000254e4
BIN/WORLD/D141BTL.EMI: 0000fce4
BIN/WORLD/D142BTL.EMI: 0000fce4
BIN/WORLD/D152BTL.EMI: 0000fce4
BIN/WORLD/E077BTL.EMI: 0000fce4
```
## Battle
During battle, the character loses 6.25% of their current HP every turn/
```
801da7f8 lw      $v0, 0x00b0(v0) ; load current HP
801da7fc lw      $v1, 0x0010(a0)
801da800 addiu   $v0, 0x0008 ; add 8 to the current HP
801da804 srl     $v0, 0x04 ; divide current HP + 8 by 16
```
The code can be found at `BIN/BATTLE/BTLMOVE.EMI: 000127f8`