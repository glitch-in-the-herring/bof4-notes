| ID           | Equipped By   | Element | Weight | Power | Hits | Shield Damage |
| ------------ | ------------- | ------- | ------ | ----- | ---- | ------------- |
| `0x13`<br>19 | Ryu<br>Fou-Lu | None    | 8      | 128   | 1    | 4             |

Not to be confused with the [[Dragonslayer]], The Dragon Blade deals 50% extra damage to dragons.
```
801d3cd4 lbu     $v1, 0x0002(v0) ; load target's type
801d3cd8 li      $v0, 0x0005
801d3cdc bne     $v1, $v0, 0x801d3cf0
801d3ce0 li      $v0, 0x004d

; If the target is a dragon
801d3ce4 sra     $v0, $s0, 0x01 ; damage / 2
801d3ce8 addu    $s0, $v0 ; damage + damage / 2
```