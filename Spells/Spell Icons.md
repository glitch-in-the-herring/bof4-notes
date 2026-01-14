Spell icons not only serve as a visual indicator for the spell's elemental affinity, but also determines whether or not two spells can combo. In a way, it serves as the "primary" type of a spell. For example, even though FlameStrike is a fire-based melee attack, it cannot be used to start a combo with a wind spell, as its spell icon is `0x2000`, or melee.

| Icon byte | Type      | Note                      |
| --------- | --------- | ------------------------- |
| `0x0000`  | "Special" | Spells such as Meditation |
| `0x0100`  | Fire      |                           |
| `0x0200`  | Wind      |                           |
| `0x0400`  | Water     |                           |
| `0x0800`  | Earth     |                           |
| `0x1000`  | Holy      |                           |
| `0x2000`  | Melee     |                           |
| `0x4000`  | Death     |                           |
| `0x8000`  | LV DWN    | Only used by [[Douse]]    |
| `0x0001`  | ST DWN    |                           |
| `0x0002`  | LV UP     |                           |
| `0x0004`  | ST UP     |                           |
| `0x0008`  | Status    |                           |
| `0x0010`  | Breath    |                           |
| `0x0020`  | "Normal"  | Spells such as Monopolize |
