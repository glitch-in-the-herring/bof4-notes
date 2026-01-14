## Normal Elemental Combos
The table can be found at:
* `BIN/BATTLE/BTLMOVE.EMI: 0001ce50` in the files
* `0x801e4e50` in the RAM
The table is divided into four entries the combos for a certain element combination. Each entry is ordered as so:
* Level 1 Combo
* Level 2 Combo
* Level 3 Combo
* Dragon Spell Combo

| Position | Description        |
| -------- | ------------------ |
| 0-3      | Fire/Wind Combos   |
| 4-7      | Wind/Water Combos  |
| 8-11     | Water/Earth Combos |
| 12-15    | Earth/Fire Combos  |
## Melee Combos
The table for Melee combos can be found at
- `BIN/BATTLE/BTLMOVE.EMI: 0001cee2` in the files
- `0x801e4ee2` in the RAM
Each entry is two bytes long. The first one determines the combo spell, while the second one determines who can cause that combo to happen. The table starts with Nina's combo.
## Spell Levels
Spells that can cause an elemental combo are listed at:
* `BIN/BATTLE/BTLMOVE.EMI: 0001ce70` in the files
* `0x801e4e70` in the RAM
The table is 82 bytes long, and contains the data for 41 spells. Each entry is two bytes long. The first byte is the spell's ID, the second byte is the spells level. The spell levels are zero-indexed, so a `0x00` in the table is in fact a level 1 spell.

## Dragon Spell Combos
Dragon spell checks are handled through a series of if-else statements:

```
801ce994 andi    $v1, $a0, 0xffff
801ce998 li      $v0, 0x00a3 ; load the spell ID for Hwajeh
801ce99c beq     $v1, $v0, 0x801ce9bc ; branch if the spell is Hwajeh
801ce9a0 li      $v0, 0x00a6 ; load the spell ID for Ahryu P'ung
801ce9a4 beq     $v1, $v0, 0x801ce9bc ; branch if the spell is Ahryu P'ung
801ce9a8 li      $v0, 0x00a9 ; load the spell ID for Pa Bing'ah
801ce9ac beq     $v1, $v0, 0x801ce9bc ; branch if the spell is Pa Bing'ah
801ce9b0 li      $v0, 0x00ac ; load the spell ID for Patoh Pah
801ce9b4 bne     $v1, $v0, 0x801ce9d0 ; branch somewhere else if the spell is not Patoh Pah

; Branch
801ce9bc jr      $ra
801ce9c0 li      $v0, 0x0003 ; set the combo offset to 3
```
The code can be found at `BIN/BATTLE/BTLMOVE.EMI: 00006994`