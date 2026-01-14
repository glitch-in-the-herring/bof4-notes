| Spell ID      | Targeting | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | --------- | --------- | ----- | --- | ------- | --------- |
| `0x68`<br>104 | Self      | Yes<br>2  | 0<br> | 0   | None    | LV UP     |
Focus is a self-buff that increases the user's ATK. It has four levels. When guarding, this level increases by one. The ATK multiplier is given by the table below:

| Level | Multiplier |
| ----- | ---------- |
| 0     | 125%       |
| 1     | 150%       |
| 2     | 175%       |
| 3     | 200%       |
The user's focus counter can be found:
* `+0x1a0` from the true start of the character's section
* `+0x104` from the character's name
* `+0x6c` from the character's modified stats subsection
This is shared with [[Concentrate]].
The multiplier table can be found at `BIN/BATTLE/BTLMOVE.EMI: 0000483c`. This table is shared with Concentrate.
The following code can be found at `BIN/BATTLE/BTLMOVE.EMI: 00010e48`
```
801d8e48 lbu     $v0, 0x006c(a0) ; load the focus level
801d8e4c lhu     $v1, 0x001e(a1) ; load the user's ATK
801d8e50 addu    $v0, $sp, $v0 ; offset + base address
801d8e54 lbu     $v0, 0x0000(v0) ; load the multiplier
801d8e58 nop     
801d8e5c mult    $v1, $v0 ; multiply the ATK by the multiplier
801d8e60 mflo    $v1, $lo
801d8e64 lui     $v0, 0x51eb
801d8e68 ori     $v0, 0x851f
801d8e6c mult    $v1, $v0
801d8e70 mfhi    $v0, $hi
801d8e74 sra     $v0, 0x05
801d8e78 sh      $v0, 0x001e(a1) ; store the new ATK
```