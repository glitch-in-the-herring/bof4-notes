The amount of buff/debuff a spell gives is determined by the stat change table for that spell. The location of a spell's stat change table is given in its notes. Each entry is 4 bytes long and is structured as such:

| Position | Description        | Value(s)                                                              | Note                   |
| -------- | ------------------ | --------------------------------------------------------------------- | ---------------------- |
| 0        | Buff/Debuff amount | 8-bit unsigned integer                                                | For spells that affect |
| 1        | Can be repeated?   | `0xff` blocks an entry from working                                   | Tentative              |
| 2        |                    |                                                                       |                        |
| 3        | Target             | `0x00`: Power<br>`0x01`: Defense<br>`0x02`: Agility<br>`0x03`: Wisdom |                        |
There seems to be another similar table for other stats.

| Position | Description      | Value(s)                                                                                                                                                        | Note                                          |
| -------- | ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| 0        | Target           | `0x00`: Focus counter<br>`0x01`: Concentrate counter<br>`0x02`: Shield<br>`0x05`: Fire resistance<br>`0x06`: Holy resistance<br>`0xff`: Remove all assist magic | Undefined values appear to affect the Shield. |
| 1        | Can be repeated? | `0xff` blocks an entry from working                                                                                                                             | Tentative                                     |
| 2        |                  |                                                                                                                                                                 |                                               |
| 3        |                  |                                                                                                                                                                 |                                               |
