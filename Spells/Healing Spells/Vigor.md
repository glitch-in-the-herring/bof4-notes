
| Spell ID     | Targeting                                     | Learnable | Power            | AP  | Element | Icon/Type |
| ------------ | --------------------------------------------- | --------- | ---------------- | --- | ------- | --------- |
| `0x30`<br>48 | All<br>Enemy or player party (front and back) | No        | 60<br>Unused<br> | 50  | Holy    | Holy      |
Second-tier multi-target heal. Its sequela is even more healing.
- As a standalone spell, the heal data can be found at:
    - `BIN/BMAGIC/MAGIC047.EMI: 0x00017824` in the files
    - `0x801ea024` in the RAM
    - Normally the power is 60 and the multiplier is 100
- The first sequela's heal data can be found at:
    - `BIN/BMAGIC/MAGIC047.EMI: 0x00017828`in the files
    - `0x801ea028` in the RAM
    - Normally the power is 60 and the multiplier is 110
- The second sequela's heal data can be found at
    - `BIN/BMAGIC/MAGIC047.EMI: 0x0001782c` in the files
    - `0x801ea02c` in the RAM
    - Normally the power is 60 and the multiplier is 130
- The third sequela's heal data can be found at
    - `BIN/BMAGIC/MAGIC047.EMI: 0x00017830 in the files
    - `0x801ea030` in the RAM
    - Normally the power is 60 and the multiplier is 25