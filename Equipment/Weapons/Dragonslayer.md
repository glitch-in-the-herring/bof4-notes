
| ID           | Equipped By  | Element | Weight | Power | Hits | Shield Damage |
| ------------ | ------------ | ------- | ------ | ----- | ---- | ------------- |
| `0x56`<br>86 | Ryu<br>Scias | None    | 15     | 70    | 1    | 7             |

The Dragonslayer is a weapon that deals additional to Ryu and Fou-Lu. How much more? *Three times*. It also deals... no extra damage to dragon-type enemies. This weapon disappears from the player's inventory after Cray kills Elina.

The code can be found at `BIN/BATTLE/BTLMOVE.EMI: 0000bca4`.
```
801d3ca4 lbu     $a1, 0x011c(v1) ; load current weapon
801d3d8c li      $v0, 0x0056
801d3dc8 bne     $a1, $v0, 0x801d3e6c
801d3dcc lui     $v0, 0x8012

; If the current weapon is a Dragonslayer
801d3dd0 lui     $v1, 0x8012
801d3dd4 lbu     $v0, -0x1ed0(v1) ; load target's index
801d3dd8 nop     
801d3ddc sltiu   $v0, 0x0006
801d3de0 beq     $v0, $r0, 0x801d3e34
801d3de4 addiu   $v1, -0x1ed0

; If the target is a party member
801d3de8 lw      $v0, 0x000c(v1)
801d3dec nop     
801d3df0 lbu     $v1, 0x00a4(v0) ; load target's ID
801d3df4 nop     
801d3df8 bne     $v1, $r0, 0x801d3e0c
801d3dfc li      $v0, 0x0006

; If the target is Ryu
801d3e00 sll     $v0, $s0, 0x01
801d3e04 addu    $s0, $v0 ; multiply damage by 3

801d3e0c bne     $v1, $v0, 0x801d3e20
801d3e10 li      $v0, 0x0007

; If the target is Fou-lu
801d3e14 sll     $v0, $s0, 0x01
801d3e18 addu    $s0, $v0 ; multiply damage by 3

801d3e1c li      $v0, 0x0007
801d3e20 bne     $v1, $v0, 0x801d3e2c

; If the target's ID is 7?
801d3e24 sll     $v0, $s0, 0x01
801d3e28 addu    $s0, $v0 ; multiply damage by 3

801d3e2c j       0x801d3e58
801d3e30 li      $v0, 0x0008
801d3e58 bne     $v1, $v0, 0x801d3e6c
801d3e5c lui     $v0, 0x8012

; If the target's ID is 8?
801d3e60 sll     $v0, $s0, 0x01
801d3e64 addu    $s0, $v0 ; multiply damage by 3
```
It's still unclear what the character IDs 7 and 8 are supposed to mean.