The available targeting options are:

| Byte   | Targeting                                                              | Note                                                                                                                                                                                             | Example      |
| ------ | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ |
| `0x00` | Self                                                                   |                                                                                                                                                                                                  | Focus        |
| `0x01` | Weapon-dependent<br>Player or enemy party                              | If the user is wielding a single-target weapon, the player's front and back rows can be targeted.<br>If the user is wielding a multi-target weapon, only the player's front row can be targeted. | Shadowwalk   |
| `0x03` | All<br>Always enemy party                                              |                                                                                                                                                                                                  | Fireblast    |
| `0x05` | All<br>Always player party (front)                                     |                                                                                                                                                                                                  | Holy Circle  |
| `0x07` | All<br>Enemy and player party (front)                                  |                                                                                                                                                                                                  | Shout        |
| `0x0d` | All<br>Always player party (front and back)                            |                                                                                                                                                                                                  | Healing Wind |
| `0x0f` | All<br>Enemy and player party (front and back)                         |                                                                                                                                                                                                  | Sanctuary    |
| `0x47` | All<br>Enemy or player party (front)                                   |                                                                                                                                                                                                  | Shield       |
| `0x4c` | Single<br>Player party only (front or back)                            |                                                                                                                                                                                                  | Resurrect    |
| `0x4e` | Single<br>Enemy or player party (front or back)                        |                                                                                                                                                                                                  | Might        |
| `0x62` | Single<br>Enemy party only                                             |                                                                                                                                                                                                  | Flare        |
| `0x67` | All<br>Enemy or player party (front)                                   |                                                                                                                                                                                                  | Mjollnir     |
| `0x6e` | Single<br>Enemy or player party (front or back)                        |                                                                                                                                                                                                  | Blunt        |
| `0xce` | Single<br>Enemy or player party (front or back)<br>Usable in the field |                                                                                                                                                                                                  | Heal         |
| `0xdf` | All<br>Enemy or player party (front and back)                          |                                                                                                                                                                                                  | Vigor        |
Terminology:

| Term                   | Meaning                                                                               |
| ---------------------- | ------------------------------------------------------------------------------------- |
| Player or enemy party  | The user can make a choice between targets in the enemy's party or the player's party |
| Player and enemy party | Every single member of both the player and enemy party are targeted                   |
| Front and back         | Both the front row and the back row of the player's party                             |
As bit switches (still tentative):

| Bit    | Function                                  | Notes |
| ------ | ----------------------------------------- | ----- |
| `0x01` | Can target all                            |       |
| `0x02` | Can target enemy party                    |       |
| `0x04` | Can target player party                   |       |
| `0x08` | Can target back row of the player's party |       |
| `0x10` |                                           |       |
| `0x20` | Initially target the enemy party          |       |
| `0x40` | Initially target the                      |       |
| `0x80` | Can be used in the field                  |       |
