When you cast spells of a certain [[Spell Icons|spell type]] one after another, then the result is an in-a-row combo. Unlike elemental combos, this does not result in a new spell being cast. Its sequela is the effect of the spell repeated.
In the combo HUD, this is indicated by the the visually smaller number next to the spell's icon.
The counter for each spell type starts at `0x8011df84` in the RAM.
The counter for breath (`0x8011df90`) is unusual in that it also gets incremented, even when no breath spell is being used. This increment comes from `0x8011df50`, the combo index.
