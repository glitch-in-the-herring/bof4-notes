| Spell ID      | Targeting                 | Learnable | Power       | AP  | Element | Icon/Type |
| ------------- | ------------------------- | --------- | ----------- | --- | ------- | --------- |
| `0xc8`<br>200 | All<br>Always enemy party | No        | 0<br>Unused | 9   | Death   | Normal    |
Depress removes 1/8 of the target's AP. It doesn't go anywhere, the caster doesn't receive any of the AP, it's just gone.
```
; ; ; ; ; ; ; ; ; ; ;
; Amount to drain   ;
; ; ; ; ; ; ; ; ; ; ;
801db92c lw      $v1, 0x0018(v0) ; load the target's AP
801db930 lw      $v0, 0x0010(v0)
801db934 srl     $v1, 0x03 ; divide by 8
801db938 sw      $v1, 0x000c(v0) ; store amount to steal
```

```
; ; ; ; ; ; ; ;
; Steal AP    ;
; ; ; ; ; ; ; ;
801d8fac lw     $v1, 0x00b4(a1); load target's AP
801d8fb0 lw     $v0, 0x000c(v0)
801d8fb4 nop    
801d8fb8 subu   $a0, $v1, $v0 ; subtract AP
...
801d9020 sw     $a0, 0x00b4(v0) ; store AP
```

#EnemyOnly