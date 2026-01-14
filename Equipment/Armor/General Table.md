The general table for armor can be found  at 
* `BIN/SYSTEM/GAME.EMI: 0000d624` in the files
* `0x8019a624` in the RAM
Starting with the empty armor. Each entry is 12 bytes long.

| Position | Description       | Value(s)                                        | Note                                                                            |
| -------- | ----------------- | ----------------------------------------------- | ------------------------------------------------------------------------------- |
| 0        |                   |                                                 |                                                                                 |
| 1        |                   |                                                 |                                                                                 |
| 2        | Armor type        | `0x0_`: Armor<br>`0x1_`: Cloth<br>`0x2_`: Dress |                                                                                 |
| 3<br>    |                   |                                                 |                                                                                 |
| 4        | Equipability      | See [[Equipability]]                            |                                                                                 |
| 5        | Weight            | 8-bit unsigned integer                          |                                                                                 |
| 6-7      | Defense           | 16-bit unsigned integer                         |                                                                                 |
| 8-9      | Description Index | 16-bit integer                                  |                                                                                 |
| 10-11    | Selling price     | 16-bit integer                                  | The purchasing price is automatically calculated by doubling the selling price. |

