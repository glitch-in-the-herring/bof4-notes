| Spell ID      | Targeting | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | --------- | --------- | ----- | --- | ------- | --------- |
| `0x69`<br>105 | Self      | Yes<br>2  | 0<br> | 0   | None    | LV UP     |
Concentrate is a self-buff that increases the user's WIS. It has four levels. When guarding, this level increases by one. The WIS multiplier is given by the table below:

| Level | Multiplier |
| ----- | ---------- |
| 0     | 125%       |
| 1     | 150%       |
| 2     | 175%       |
| 3     | 200%       |
The user's concentrate counter can be found:
* `+0x1a0` from the true start of the character's section
* `+0x104` from the character's name
* `+0x6c` from the character's modified stats subsection
This is shared with [[Focus]].
The multiplier  table can be found at `BIN/BATTLE/BTLMOVE.EMI: 0000483c`. This table is shared with Focus.
The following code can be found at `BIN/BATTLE/BTLMOVE.EMI: 00010e90`
```
801d8e90 lbu     $v0, 0x006c(a0) ; load the concentrate level
801d8e94 lhu     $v1, 0x0024(a1) ; load the attacker's WIS
801d8e98 addu    $v0, $sp, $v0 ; offset + base address
801d8e9c lbu     $v0, 0x0000(v0) ; load the multiplier
801d8ea0 nop     
801d8ea4 mult    $v1, $v0 ; multiply the WIS by the multiplier
801d8ea8 mflo    $v1, $lo
801d8eac lui     $v0, 0x51eb
801d8eb0 ori     $v0, 0x851f
801d8eb4 mult    $v1, $v0
801d8eb8 mfhi    $v0, $hi
801d8ebc sra     $v0, 0x05
801d8ec0 sh      $v0, 0x0024(a1) ; store the new WIS
```