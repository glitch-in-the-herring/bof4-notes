For most buffs/debuffs, the spell does not modify the stat directly, but rather a multiplier. This multiplier is multiplied to the target's final stats (in the case of the player's party, the stat after all equipment has been accounted). Each multiplier is an 8-bit unsigned integer value, interpreted as percent values.
* `+0x18c` from the true start of the character's section
* `+0xf0` from the character's name
* `+0x58` from the character's modified stats subsection
They follow the normal order of stats:
* PWR
* DEF
* AGL
* WIS
* ??
* ??
* ??
* ??
The increase given by the buff is stored first into the [[Battle Global Temporary 8-Bit Values]]. 