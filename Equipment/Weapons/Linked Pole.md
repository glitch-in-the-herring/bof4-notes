| ID           | Equipped By | Element | Weight | Power | Hits | Shield Damage |
| ------------ | ----------- | ------- | ------ | ----- | ---- | ------------- |
| `0x39`<br>57 | Cray        | None    | 8      | 133   | 1    | 4             |
Its description is slightly misleading: It does not scale with target's actual PWR (the stat), instead it looks at whether the target's level is less or greater than the attacker's level.
$$
d' = \begin{cases}
d - \left\lfloor\frac{d}{4}\right\rfloor & L_A  < L_D\\
d + \left\lfloor\frac{d}{4}\right\rfloor & L_A \geq L_D
\end{cases}
$$