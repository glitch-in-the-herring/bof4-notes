In-battle HP Regeneration comes from two sources: equipment and innate regeneration.
## Equipment-Based Regeneration
Three equipment grant in-battle regeneration:
* Life Armor: +100/turn
* Cupid's Lyre: +50/turn
* Ivory Bangle: +150/turn
### File
The code that governs regeneration is found in `BIN/BATTLE/BTLMOVE.EMI`. All of the file addresses below refer to addresses in `BTLMOVE.EMI`.
The code that checks this can be found starting at `0x0001128b8`:
* The part that checks for Life Armor can be found at `0x00012944`. Normally this is `0x11`.
	* The part that determines the amount of HP healed by Life Armor can be found at `0x00012960`. Normally this is -100.
* The part that checks for Cupid's Lyre can be found at `0x0001298c`. Normally this is `0x18`.
	* The part that determines the amount of HP healed by Cupid's Lyre can be found at `0x000129a8`. Normally this is -50.
* The part that checks for Ivory Bangle can be found at `0x000129d4`. Normally this is `0x19`.
	* The part that determines the amount of HP healed by Ivory Bangle can be found at `0x000129f0`. Normally this is -150
### RAM
The code starts at `0x801da8b8`:
* The part that checks for Life Armor can be found at `0x801da944`.
	* The part that determines the amount of HP healed by Life Armor can be found at `0x801da960`.
* The part that checks for Cupid's Lyre can be found at `0x801da98c`.
	* The part that determines the amount of HP healed by Cupid's Lyre can be found at `0x801da9a8`.
* The part that checks for Ivory Bangle can be found at `0x801da9d4`.
	* The part that determines the amount of HP healed by Ivory Bangle can be found at `0x801da9f0`.

## Innate Regeneration
Innate regeneration only happens with enemies. This normally regenerates 50% of their HP. The code that determines this can be found at `0x00012900`.