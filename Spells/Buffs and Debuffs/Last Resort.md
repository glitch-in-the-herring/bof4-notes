
| Spell ID      | Targeting | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | --------- | --------- | ----- | --- | ------- | --------- |
| `0x6d`<br>109 | Self      | Yes<br>4  | 0<br> | 0   | None    | ST UP     |
Last Resort converts the user's DEF to ATK, reducing DEF to 0. The following code can be found at `BIN/SYSTEM/GAME.EMI: 00009b10`.
```
80196b10 lhu     $v0, 0x00de(s0) ; load the target's ATK
80196b14 lhu     $v1, 0x00e0(s0) ; load the target's DEF
80196b18 sh      $r0, 0x00e0(s0) ; set the target's DEF to 0
80196b1c addu    $v0, $v1 ; add the target's DEF to the target's ATK
80196b20 sh      $v0, 0x00de(s0) ; store the target's new ATK
```