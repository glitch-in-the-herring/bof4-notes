The general table for accessories is can be found at at 
- `/BIN/SYSTEM/GAME.EMI: 0000d96c` in the files
- `0x8019a96c` in the RAM
starting with the nothing accessory. Each entry is 12 bytes long and can be broken down as such:

| Position | Description       | Value(s)                                                                                | Note                                                                    |
| -------- | ----------------- | --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| 0        |                   |                                                                                         |                                                                         |
| 1        |                   |                                                                                         |                                                                         |
| 2        | Icon/Type         | `0x0_`: Ring<br>`0x1_`: Boots<br>`0x2_`: Helmet<br>`0x3_`: Fishing pole<br>`0x4_`: Bait |                                                                         |
| 3        |                   |                                                                                         |                                                                         |
| 4        | Equipability      | See [[Equipability]]                                                                    |                                                                         |
| 5        | Weight            | 8-bit unsigned integer                                                                  |                                                                         |
| 6-7      | Defense           | 16-bit unsigned integer                                                                 |                                                                         |
| 8-9      | Description Index | 16-bit unsigned integer                                                                 |                                                                         |
| 10-11    | Selling price     | 16-bit unsigned integer                                                                 | The purchasing price is automatically calculated as twice of this value |

