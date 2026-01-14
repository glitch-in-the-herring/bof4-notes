
| Spell ID      | Targeting                 | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | ------------------------- | --------- | ----- | --- | ------- | --------- |
| `0xca`<br>202 | All<br>Always enemy party | No        | 15    | 15  | None    | Breath    |
For the damage formula see [[Breath Formula#Primus]]

## Hit count
Primus deals eight hits. The following code can be found at `BIN/BMAGIC/MAGIC202.EMI: 00010db0`:
```
801e6db0 li     $v1, 0x0008 ; load the number of hits
801e6db4 lbu    $v0, 0x0005(s1)
801e6db8 sb     $v1, 0x004e(s1) ; store the number of hits
801e6dbc addiu  $v0, 0x0001
801e6dc0 sb     $v0, 0x0005(s1)
801e6dc4 lui    $v0, 0x8012
801e6dc8 addiu  $a0, $v0, -0x20d0 
801e6dcc sb     $v1, 0x0189(a0) ; store the number of hits
```
See [[Distributed Hits]] for more information.
### Sequelae
As the second spell in a combo chain, Primus deals 11 hits:
```
801e6dec li     $v0, 0x000b ; load the number of hits
801e6df0 sb     $v0, 0x0189(a0) ; store the number of hits
```
The code can be found at `BIN/BMAGIC/MAGIC202.EMI: 00010dec`
As the third spell in a combo chain, Primus deals 14 hits, which is calculated as 8 + 6:
```
; what precedes this is the same code that sets 8 as the hit count
801e6e04 lbu    $v0, 0x0189(a0) ; load the number of hits
801e6e08 nop    
801e6e0c addiu  $v0, 0x0006 ; add 6 to the number of hits
801e6e10 sb     $v0, 0x0189(a0) ; store the number of hits
```