| ID           | Equipped By | Element | Weight | Power | Hits | Shield Damage |
| ------------ | ----------- | ------- | ------ | ----- | ---- | ------------- |
| `0x1c`<br>28 | Ershin      | None    | 10     | 119   | 1    | 5             |
The Homing Bomb skips the accuracy check and frequent dodges check
```
801def1c lbu    $v1, 0x011c(a0) ; load weapon ID
801def20 li     $v0, 0x0048 ; load the Homing Bomb's ID
801def24 beq    $v1, $v0, 0x801def50
801def28 li     $v0, 0x0009
; if the weapon is the Homing Bomb
801def50 j      0x801df05c ; skip checks
```
The code can be found at `BIN/BATTLE/BTLMOVE.EMI: 00016f1c`