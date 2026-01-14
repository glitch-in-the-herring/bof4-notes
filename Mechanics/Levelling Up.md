The level-up tables can be found at
* in the files
* in the RAM
Each character's table is 100 entries long, each entry being 8 bytes long, starting with Ryu's level 0 entry. The entries represent the stat change for the *next* level, not the current one. It is structured as such:

| Position | Description                  | Value(s)                                         | Note                                                             |
| -------- | ---------------------------- | ------------------------------------------------ | ---------------------------------------------------------------- |
| 0-1      | XP requirement               | 16-bit unsigned integer                          | Multiply by 2 to get the actual amount of EXP needed to level up |
| 2        | HP increase                  | 8-bit unsigned integer                           |                                                                  |
| 3        | AP increase<br>CP increase   | 4-bit unsigned integer<br>4-bit unsigned integer | The first digit is for AP<br>The second digit is for CP          |
| 4        | PWR increase<br>DEF increase | 4-bit unsigned integer<br>4-bit unsigned integer | The first digit is for PWR<br>The second digit is for DEF        |
| 5        | AGL increase<br>WIS increase | 4-bit unsigned integer<br>4-bit unsigned integer | The first digit is for AGL<br>The second digit is for WIS        |
| 6        | New ability                  | 8-bit unsigned integer                           | ID of the spell that the character learns                        |
| 7        | Latent ability?              | 8-bit unsigned integer                           | ID of the spell that the character learns, only used by Ershin?  |
