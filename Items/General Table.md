The general table for items is can be found at at 
- `/BIN/SYSTEM/GAME.EMI: 0000cd9c` in the files
- `0x80199d9c` in the RAM
starting with the nothing item. Each entry is 8 bytes long and can be broken down as such:

| Position | Description       | Value(s)                      | Note                                                                    |
| -------- | ----------------- | ----------------------------- | ----------------------------------------------------------------------- |
| 0        | Targeting         | See [[Targeting]]             | Identical to spell targeting                                            |
| 1        |                   |                               |                                                                         |
| 2        | Icon/Type         | `0x0_`: Pouch<br>`0x1_`: Fish |                                                                         |
| 3        | Power             | 8-bit unsigned integer        | Not all items use this                                                  |
| 4-5      | Description index | 16-bit unsigned integer       |                                                                         |
| 6-7      | Selling price     | 16-bit unsigned integer       | The purchasing price is automatically calculated as twice of this value |