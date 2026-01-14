Whenever you attack an NPC with Ryu, Ershin's or Ursula's field actions, you lose one game point. It's not a lot but it is objectively a bad feature because now free zenny is no longer "free" and the illusion of a penalty is imposed to the player. Do you do the wrong thing to profit yourself or do you avoid it?

For some reason the code for the penalty caused by Ryu and Ershin's field actions are separate from Ursula's, probably because hers is a ranged attack. This part is shared by the two groups:
```
...
80196034 lui     $v0, 0x8012
80196038 addiu   $a1, $v0, -0x56b4
8019603c lw      $v0, 0x0e18(a1) ; load current game points
80196040 nop     
80196044 addu    $v1, $v0, $a0 ; subtract $a0 from current game points
80196048 bgez    $v1, 0x8019605c

; If the new amount of game points is greater than or equal to 0
8019604c sw      $v1, 0x0e18(a1) ; store the new game points

; If the new amount is negative
80196050 sw      $r0, 0x0e18(a1) ; force it to be 0
```
This code can be found at `BIN/SYSTEM/GAME.EMI: 00009034`.
## Ryu and Ershin

```
801dc048 li      $a0, -0x0001 ; load -1 to $a0; 
```
### Locations
```
BIN/BATTLE/BTLRET.EMI: 00014848
BIN/SYSTEM/FLD_MAIN.EMI: 0002a048
BIN/WORLD/D141BTL.EMI: 00014848
BIN/WORLD/D142BTL.EMI: 00014848
BIN/WORLD/D152BTL.EMI: 00014848
BIN/WORLD/E077BTL.EMI: 00014848
```
## Ursula
```
801dc380 li     $a0, -0x0001 ; load -1 to $a0; 
```
### Locations

```
BIN/BATTLE/BTLRET.EMI: 00014b80
BIN/SYSTEM/FLD_MAIN.EMI: 0002a380
BIN/WORLD/D141BTL.EMI: 00014b80
BIN/WORLD/D142BTL.EMI: 00014b80
BIN/WORLD/D152BTL.EMI: 00014b80
BIN/WORLD/E077BTL.EMI: 00014b80
```