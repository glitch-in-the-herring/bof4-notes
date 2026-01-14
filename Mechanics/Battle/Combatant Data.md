Combatant data starts at `0x801c79b8` in the RAM and is 420 bytes long for each combatant. 

| Position | Description | Value(s)                     | Note |
| -------- | ----------- | ---------------------------- | ---- |
| 0-7      | Name        | ASCII null-terminated string |      |
| 10-11    | Level       | 16-bit unsigned integer      |      |
| 12-15    | EXP         | 32-bit signed integer        |      |

## Stats section
The stats section starts at `+0xd4` from the start of the combatant data.

| Position | Description              | Value(s)                       | Note                                                                                                                                                                       |
| -------- | ------------------------ | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0-3      | Current HP               | 32-bit signed integer          |                                                                                                                                                                            |
| 4-7      | Current AP               | 32-bit signed integer          |                                                                                                                                                                            |
| 24-27    | Current max HP           | 32-bit signed integer          | Current max HP drops when the party member is knocked out mid-battle and is not revived during the battle. It is restored back to the true max HP after resting in an inn. |
| 28-31    | Current max AP           | 32-bit signed integer          |                                                                                                                                                                            |
| 32-33    | Effective CP             | 16-bit unsigned integer        | This is the combatant's CP after all equipment modifiers.                                                                                                                  |
| 34-35    | Effective PWR            | 16-bit unsigned integer        | This is the combatant's PWR after all equipment modifiers and buffs/debuffs.                                                                                               |
| 36-37    | Effective DEF            | 16-bit unsigned integer        | This is the combatant's DEF after all equipment modifiers and buffs/debuffs.                                                                                               |
| 38-39    | Effective AGL            | 16-bit unsigned integer        | This is the combatant's AGL after all equipment modifiers and buffs/debuffs.                                                                                               |
| 40-41    | Effective WIS            | 16-bit unsigned integer        | This is the combatant's WIS after all equipment modifiers and buffs/debuffs.                                                                                               |
| 42-53    | Effective resistances    | 8-bit unsigned integers        | This is the combatant's resistances after all equipment modifiers and buffs/debuffs.<br>See [[Resistance]] for the order of resistances.                                   |
| 54       | Effective learning rate  | 8-bit unsigned integer         | This is the combatant's learning rate after all equipment modifiers and buffs/debuffs.<br>See [[Learning]] for information about how this is used.                         |
| 55       | Effective counter rate   | 8-bit unsigned integer         | This is the combatant's counter rate after all equipment modifiers and buffs/debuffs.                                                                                      |
| 56       | Effective critical rate  | 8-bit unsigned integer (0-100) | This is the combatant's critical rate after all equipment modifiers and buffs/debuffs.                                                                                     |
| 57       | Effective dodge rate     | 8-bit unsigned integer (0-100) | This is the combatant's dodge rate after all equipment modifiers and buffs/debuffs.                                                                                        |
| 58       | Effective alertness rate | 8-bit unsigned integer (0-100) | This is the combatant's alertness rate after all equipment modifiers.                                                                                                      |
| 59       | Effective accuracy       | 8-bit unsigned integer (0-100) | This is the combatant's accuracy after all equipment modifiers and buffs/debuffs.                                                                                          |
| 24-27    | True max HP              | 32-bit signed integer          |                                                                                                                                                                            |
| 28-31    | True max AP              | 32-bit signed integer          |                                                                                                                                                                            |
| 32-33    | True CP                  | 16-bit unsigned integer        | This is the combatant's CP without equipment modifiers. Levelling up directly increases this stat.                                                                         |
| 34-35    | Base PWR                 | 16-bit unsigned integer        | This is the combatant's PWR without any equipment modifiers and buffs/debuffs. Levelling up or using permanent stat increasing items directly increases this stat.         |
| 36-37    | Base DEF                 | 16-bit unsigned integer        | This is the combatant's DEF without any equipment modifiers and buffs/debuffs. Levelling up or using permanent stat increasing items directly increases this stat.         |
| 38-39    | Base AGL                 | 16-bit unsigned integer        | This is the combatant's AGL without any equipment modifiers and buffs/debuffs. Levelling up or using permanent stat increasing items directly increases this stat.         |
| 40-41    | Base WIS                 | 16-bit unsigned integer        | This is the combatant's WIS without any equipment modifiers and buffs/debuffs. Levelling up or using permanent stat increasing items directly increases this stat.         |
| 42-53    | Base resistances         | 8-bit unsigned integers        | This is the combatant's resistances without any equipment modifiers and buffs/debuffs.<br>See [[Resistance]] for the order of resistances                                  |
| 54       | Base learning rate       | 8-bit unsigned integer         | This is the combatant's learning rate without any equipment modifiers and buffs/debuffs.<br>See [[Learning]] for information about how this is used                        |
| 55       | Base counter rate        | 8-bit unsigned integer         | This is the combatant's counter rate without any equipment modifiers and buffs/debuffs.                                                                                    |
| 56       | Base critical rate       | 8-bit unsigned integer (0-100) | This is the combatant's critical rate without any equipment modifiers and buffs/debuffs.                                                                                   |
| 57       | Base dodge rate          | 8-bit unsigned integer (0-100) | This is the combatant's dodge rate without any equipment modifiers and buffs/debuffs.                                                                                      |
| 58       | Base alertness rate      | 8-bit unsigned integer (0-100) | This is the combatant's alertness rate without any equipment modifiers and buffs/debuffs.                                                                                  |
| 59       | Base accuracy            | 8-bit unsigned integer (0-100) | This is the combatant's accuracy without any equipment modifiers and buffs/debuffs.                                                                                        |
| 60       | Weapon                   | 8-bit unsigned integer         |                                                                                                                                                                            |
| 61       | Armor                    | 8-bit unsigned integer         |                                                                                                                                                                            |
| 62       | Accessory                | 8-bit unsigned integer         |                                                                                                                                                                            |
| 63       | ?                        |                                |                                                                                                                                                                            |
| 64       | Master                   | 8-bit unsigned integer         | See [[Masters]]                                                                                                                                                            |
## Multipliers section
See [[Stat Multiplier]]