| Spell ID      | Targeting                                 | Learnable | Power | AP  | Element | Icon/Type |
| ------------- | ----------------------------------------- | --------- | ----- | --- | ------- | --------- |
| `0x8b`<br>139 | Weapon-dependent<br>Player or enemy party | Yes<br>3  | 0     | 2   | Normal  | Melee     |
Coward's way replaces the attacker's power with the following calculation:
$$
PWR_A'=PWR_A+\min\{L_A, E\}
$$
Where
* $PWR_A$ is the attacker's original PWR
* $L_A$ is the attacker's level
* $E$ is the number of [[escape|escapes]] the party has made.

