Escaping has a chance to remove the party from the ongoing battle.
## Success
An escape's outcome is determined by the following formula:
$$
\begin{cases}
\mathrm{Success} & \mathrm{random}(0,16)\geq \\
\mathrm{Failure}& \mathrm{random}(0,16)< 
\end{cases}
$$
$$
AGLP=\sum_{i=1}^{3} AGL_{P_i}
$$
$$
AGLE=\sum_{i=1}^{9} AGL_{E_i}
$$
$$
\Delta AGL = AGLP-AGLE + 32
$$
$$
I = \begin{cases}
0 & \Delta AGL < 0\\
\left\lfloor\frac{\Delta AGL}{8}\right\rfloor & 0 < \Delta AGL \leq 97\\
13 & \Delta AGL > 97
\end{cases}
$$

| $I$ | $S$ |
| --- | --- |
| 0   | 7   |
| 1   | 8   |
| 2   | 8   |
| 3   | 9   |
| 4   | 9   |
| 5   | 10  |
| 6   | 11  |
| 7   | 12  |
| 8   | 12  |
| 9   | 13  |
| 10  | 13  |
| 11  | 13  |
| 12  | 13  |
| 13  | 14  |
$$
\alpha = \begin{cases}
S & \mathcal{E} \neq 1\\
S + 2 & \mathcal{E} = 1\\
\end{cases}
$$
$$

$$
## Counter
The number of escapes is kept track at
* `0x8011b72e` in the RAM
* `+0xf60` in the save file
An escape is counted if the player uses the escape action and successfully executes it.
