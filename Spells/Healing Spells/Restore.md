| Spell ID     | Targeting                                                                        | Learnable | Power             | AP  | Element | Icon/Type |
| ------------ | -------------------------------------------------------------------------------- | --------- | ----------------- | --- | ------- | --------- |
| `0x2e`<br>46 | `0xce`<br>Single<br>Enemy or player party (front or back)<br>Usable in the field | No        | 120<br>Unused<br> | 18  | Holy    | Holy      |
Third-tier single target heal. Its sequela is even more healing.
- As a standalone spell, the heal data can be found at:
    - `BIN/BMAGIC/MAGIC044.EMI 0x00017108` in the files
    - `0x801ea108` in the RAM
    - Normally the power is 120 and the multiplier is 100
- The first sequela's heal data can be found at:
    - `BIN/BMAGIC/MAGIC044.EMI 0x0001710c`in the files
    - `0x801ea10c` in the RAM
    - Normally the power is 120 and the multiplier is 110
- The second sequela's heal data can be found at
    - `BIN/BMAGIC/MAGIC044.EMI 0x00017110 in the files
    - `0x801ea110` in the RAM
    - Normally the power is 120 and the multiplier is 130
- The third sequela's heal data can be found at
    - `BIN/BMAGIC/MAGIC044.EMI 0x00017114` in the files
    - `0x801ea114` in the RAM
    - Normally the power is 120 and the multiplier is 25