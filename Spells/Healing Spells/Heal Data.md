The amount of healing a spell gives is determined by the heal table for that spell. The location of a healing spell's heal change table is given in its notes. Each entry is 4 bytes long and is structured as such:

| Position | Description | Value(s)                                                                                                                        | Note |
| -------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------- | ---- |
| 0        | Multiplier  | 8-bit unsigned integer                                                                                                          |      |
| 1        |             |                                                                                                                                 |      |
| 2        | Power       | 8-bit signed<br>Anything negative seems to heal to the max HP, but `0xff` should probably be the preferred value for this case. |      |
| 3        |             |                                                                                                                                 |      |
