Wills are special actions the party members can perform. They are not triggered manually by the player. There are two main types of wills:
* Innate wills: An innate will is a will that a character has by default and cannot be replaced.
* Master wills: A master will is a will that can only be activated when a character is apprenticed under a master.
Under the hood, some of the wills are spells. When cast, Wills consume AP. Therefore, all of the will spells have their AP cost set to 0.
## Innate Wills
### Ryu
None.
### Nina
Nina's will. [[Cheering]], heals all party members.
This can be changed at `BIN/BATTLE/BTLMOVE.EMI: 00009bc8`.
### Cray
### Scias
### Ursula
### Ershin
Ershin's will, [[CoveringFire]], deals a normal attack to a single target in the enemy party.
This can be changed at `BIN/BATTLE/BTLMOVE.EMI: 00009cc4`.
### Fou-Lu
None.
## Master Wills
### Rwolf
Rwolf's will takes the average SPD of the front row party members and adds that to the front row party members.
### Una
Una's will adds 25% to the party member's physical damage, but reduces their accuracy by 10pt. The code can be found at `BIN/BATTLE/BTLMOVE.EMI: 000111d4` in the game's files"
```
801d91d4 8c43000c: lw     $v1(00000008), 0x000c(v0)([801c71ec] = 00000c6b) ; base damage
801d91d8 00000000: nop    
801d91dc 00032083: sra    $a0(801c79b8), $v1(00000c6b), 0x02 ; divide base damage by 4
801d91e0 00641821: addu   $v1(00000c6b), $a0(0000031a) ; 125% base damage
801d91e4 ac43000c: sw     $v1(00000f85), 0x000c(v0)([801c71ec] = 00000c6b) ; store damage
```
## Abbess
The Abbess' will, Reck, increases the learning rate of the party members apprenticed under her. However, this does not reflect as an immediate increase in the learning rate stat. Rather, a +75 bonus is applied to the learning rate when the learning roll is calculated. 
For the code, see [[Learning]].
