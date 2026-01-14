Rusted Sword:

| ID           | Equipped By            | Element | Weight | Power | Hits | Shield Damage |
| ------------ | ---------------------- | ------- | ------ | ----- | ---- | ------------- |
| `0x53`<br>83 | Ryu<br>Scias<br>Fou-Lu | None    | 2      | 40    | 1    | 2             |
Slayer:

| ID           | Equipped By            | Element | Weight | Power | Hits | Shield Damage |
| ------------ | ---------------------- | ------- | ------ | ----- | ---- | ------------- |
| `0x84`<br>84 | Ryu<br>Scias<br>Fou-Lu | None    | 4      | 80    | 2    | 2             |
The Rusted Sword is a weapon that can only be obtained from either Teepo in Chek after the game is cleared, or through the second Manillo in the Dengeki Store. Every enemy killed by the Rusted Sword adds to a counter. When this counter is greater than or equal to 1000, it turns into the Slayer, a much better weapon.

The Slayer is a weapon that deals two hits with every attack and steals some of the enemy's HP to the weapon's wielder. It has a ... chance to attack a party member instead of the enemy.

## Rusted Sword to Slayer
The kill counter for the Rusted Sword is stored at
* `0x8011b6ba` in the RAM
* `+0xeec` in the memory card
It is normally impossible to have multiple copies of the Rusted Sword in a normal game. However, if one were to equip additional party members with it, then kills made by any party member wielding the rusted sword will increment this counter. The catch is that only the party member who deals the final kill(s) will get their Rusted Sword converted into a Slayer.

To increment the counter, first the game checks whether or not the weapon used is a Rusted Sword. If it is, it activates a flag located at `0x8011deec` in the RAM:
```
801d95a4 lbu    $v1, 0x011c(v0) ; get the current party member's weapon
801d95a8 li     $v0, 0x0053 ; 0x53 is the ID of Rusted Sword
801d95ac bne    $v1, $v0, 0x801d95d0
801d95b0 lui    $v1, 0x8012

; if the party member is using a Rusted Sword
801d95b4 lui    $v0, 0x8012
801d95b8 addiu  $v0, -0x212c
801d95bc lw     $v1, 0x0018(v0) ; load the flag bytes
801d95c0 lui    $a0, 0x0080 
801d95c4 or     $v1, $a0 ; set the 0x0080 flag
801d95c8 sw     $v1, 0x0018(v0) ; store the new flag bytes
```
Several frames later the counter is incremented:
```
801b723c lw     $v0, 0x0018(s0) ; loaad flag bytes
801b7240 lui    $v1, 0x0080
801b7244 and    $v0, $v1
801b7248 beqz   $v0, 0x801b7264 
801b724c li     $v0, 0x0001

; if the flag for Rusted Sword is active
801b7250 lhu    $v0, 0x0d6e(a0)
801b7254 nop    
801b7258 addiu  $v0, 0x0001 ; add 1 to counter
801b725c sh     $v0, 0x0d6e(a0) ; store new counter value
```
When the counter reaches 1000 or more, the current party member's weapon is replaced with the Slayer if it is currently the Rusted Sword:
```
801cff20 lhu    $v0, 0x0d6e(s0) ; load the counter
801cff24 nop    
801cff28 sltiu  $v0, 0x03e8
801cff2c bnez   $v0, 0x801cffc0
801cff30 lui    $v0, 0x8012

; if the counter is greater than or equal to 1000
801cff34 lui    $a1, 0x8012
801cff38 lbu    $v0, -0x1f40(a1)
801cff3c nop    
801cff40 sltiu  $v0, 0x0006
801cff44 beqz   $v0, 0x801cffbc
801cff48 lui    $a0, 0x801c
801cff4c lbu    $v0, -0x1f40(a1)
801cff50 addiu  $a0, 0x79b8
801cff54 sll    $v1, $v0, 0x03
801cff58 subu   $v1, $v0
801cff5c sll    $v0, $v1, 0x04
801cff60 subu   $v0, $v1
801cff64 sll    $v0, 0x02
801cff68 addu   $a0, $v0, $a0
801cff6c lbu    $v1, 0x011c(a0) ; load current weapon
801cff70 li     $v0, 0x0053 ; 0x53 is rusted sword's ID
801cff74 bne    $v1, $v0, 0x801cffc0
801cff78 lui    $v0, 0x8012

; if the current weapon is a Rusted Sword
801cff7c li     $v0, 0x0054 ; 0x54 is Slayer's ID
801cff80 sb     $v0, 0x011c(a0) ; set Slayer as the party member's weapon
```

## Slayer's HP Stealing Ability
For each hit, the Slayer steals 1/8 of the damage dealt to the enemy + 4 extra damage points and gives it to the wielder. This is determined by the code at `BIN/BATTLE/BTLMOVE.EMI: 000112a4`:
```
801d92a4 lbu    $v1, 0x011c(v0) ; load the current character's weapon
801d92a8 li     $v0, 0x0054 ; Slayer's ID
801d92ac bne    $v1, $v0, 0x801d9320 

; If the current character's weapon is the slayer
801d92bc lw     $v0, 0x000c(v0) ; load the damage dealt for the current hit 
801d92c0 nop    
801d92c4 addiu  $a2, $v0, 0x0004 ; add 4 extra points to the damage
801d92c8 bgez   $a2, 0x801d92d4
801d92cc nop    

; If the damage dealt is positive
801d92d4 lw     $a0, 0x000c(s1) ; load the base address of the current party member
801d92d8 sra    $a2, 0x03 ; divide the damage dealt by 8
801d92dc lw     $v0, 0x00b0(a0) ; load current HP
801d92e0 lw     $a1, 0x00d4(a0) ; load max HP
801d92e4 addu   $v1, $v0, $a2 ; add the stolen HP
801d92e8 slt    $v0, $a1, $v1 
801d92ec beqz   $v0, 0x801d92f8

; If the damage dealt is less than the max hp
801d92f0 nop    
801d92f8 sw     $v1, 0x00b0(a0) ; store new HP
```
## Randomly Hitting Party Members
First, the game rolls to determine whether or not reverse targetting will be activate. If it is, then the game rolls to decide who to attack instead of the player's chosen target. The code can be found at `BIN/BATTLE/BTLMOVE.EMI: 0000d838`. 
```
801d5838  jal    0x8016f384 ; call rand()
801d583c  nop    
...
801d5840  andi   $v0, 0x000f ; random(0, 15)
801d5844  bnez   $v0, 0x801d5874 
801d5848  lui    $a0, 0x801c

; if the random number is 0
...
801d6004 jal    0x8016f384 ; call rand()
801d6008 nop    
...
801d603c addu   $v0, $sp, $v1 ; base address + random offset between 1 and number of party members (besides attacker) in the front row
801d6040 lbu    $v0, 0x0010(v0) ; load the target's index
...
801d5864 sb     $v1, -0x1f08(v0) ; change target
```