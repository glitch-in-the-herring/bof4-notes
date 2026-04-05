Field party data can be found at:
* `0x8011a94c` in the RAM
* `+0x106` in the save file

| Position | Description              | Value(s)                       | Note |
| -------- | ------------------------ | ------------------------------ | ---- |
| 0-7      | Name                     | ASCII null-terminated string   |      |
| 10-11    | Level                    | 16-bit unsigned integer        |      |
| 12-15    | EXP                      | 32-bit signed integer          |      |
| 20-23    | Current HP               | 32-bit signed integer          |      |
| 24-27    | Current AP               | 32-bit signed integer          |      |
| 30-47    | Magic spells             | 8-bit unsigned integers        |      |
| 48-55    | Skills                   | 8-bit unsigned integers        |      |
| 56-59    | Current max HP           | 32-bit signed integer          |      |
| 60-63    | Current max AP           | 32-bit signed integer          |      |
| 64-65    | Current CP               | 16-bit unsigned integer        |      |
| 66-67    | Effective PWR            | 16-bit unsigned integer        |      |
| 68-69    | Effective DEF            | 16-bit unsigned integer        |      |
| 70-71    | Effective AGL            | 16-bit unsigned integer        |      |
| 72-73    | Effective WIS            | 16-bit unsigned integer        |      |
| 74-85    | Effective resistances    | 8-bit unsigned integers        |      |
|          | Effective learning rate  | 8-bit unsigned integer         |      |
|          | Effective counter rate   | 8-bit unsigned integer         |      |
|          | Effective critical rate  | 8-bit unsigned integer (0-100) |      |
|          | Effective dodge rate     | 8-bit unsigned integer (0-100) |      |
|          | Effective alertness rate | 8-bit unsigned integer (0-100) |      |
|          | Effective accuracy       | 8-bit unsigned integer (0-100) |      |
