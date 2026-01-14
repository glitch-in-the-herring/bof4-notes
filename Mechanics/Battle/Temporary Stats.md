Some stats are not loaded directly from their actual location, but rather from a copy.
## Attacker's stats
The stats of the attacker starts at `0x8011e0d4`

| Position | Description              | Value                                           |
| -------- | ------------------------ | ----------------------------------------------- |
| 0-3      | Attacker's max? HP       | 32-bit unsigned integer                         |
| 4-5      | Attacker's max? AP       | 16-bit unsigned integer                         |
| 6        |                          |                                                 |
| 7        |                          |                                                 |
| 8        |                          |                                                 |
| 9        |                          |                                                 |
| 10-11    | Attacker's PWR           | 16-bit unsigned integer                         |
| 12-13    | Attacker's DEF           | 16-bit unsigned integer                         |
| 14-15    | Attacker's AGL           | 16-bit unsigned integer                         |
| 16-17    | Attacker's INT           | 16-bit unsigned integer                         |
| 18-29    | Attacker's resistances   | See [[Resistance]] for the values and the order |
| 30       | Attacker's learning rate | See [[Learning]]                                |
| 31       | Attacker's counter rate  |                                                 |
| 32       | Attacker's critical rate |                                                 |
| 33       | Attacker's dodge rate    |                                                 |
| 34       | Attacker's alertness     |                                                 |
| 35       | Attacker's hit rate      |                                                 |
## Defender's stats
The stats of the defender starts at `0x8011e144`.

| Position | Description            | Value                                           |
| -------- | ---------------------- | ----------------------------------------------- |
| 0-3      | Defender's max? HP     | 32-bit unsigned integer                         |
| 4-5      | Defender's max? AP     | 16-bit unsigned integer                         |
| 6        |                        |                                                 |
| 7        |                        |                                                 |
| 8        |                        |                                                 |
| 9        |                        |                                                 |
| 10-11    | Defender's PWR         | 16-bit unsigned integer                         |
| 12-13    | Defender's DEF         | 16-bit unsigned integer                         |
| 14-15    | Defender's AGL         | 16-bit unsigned integer                         |
| 16-17    | Defender's INT         | 16-bit unsigned integer                         |
| 18-29    | Defender's resistances | See [[Resistance]] for the values and the order |

#RAM