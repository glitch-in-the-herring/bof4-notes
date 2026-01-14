$$
d = \left\lfloor \frac{R(\epsilon)}{100}\right\rfloor
$$
$$
\alpha = \left\lfloor\frac{1000P(100 + WIS_A)}{100}\right\rfloor
$$
$$
\beta = \begin{cases}
100 - \left\lfloor\frac{WIS_D}{5}\right\rfloor & 100 - \left\lfloor\frac{WIS_D}{5}\right\rfloor \geq 50 \\
50 & 100 - \left\lfloor\frac{WIS_D}{5}\right\rfloor < 50
\end{cases}
$$
$$
\gamma = \left\lfloor\frac{\left\lfloor\frac{\alpha\beta}{100}\right\rfloor}{5000}\right\rfloor
$$
$$
\delta = \begin{cases}
\left\lfloor\displaystyle\frac{(100-\gamma)\left\lfloor\frac{\alpha\beta}{100}\right\rfloor}{100}\right\rfloor & 100 - \gamma \geq 80\\[1em]
\left\lfloor\displaystyle\frac{80\left\lfloor\frac{\alpha\beta}{100}\right\rfloor}{100}\right\rfloor & 100 - \gamma < 80
\end{cases}
$$
$$
\epsilon = \left\lfloor\frac{\delta\mathrm{random}(90,110)}{100}\right\rfloor
$$

* $P$ is the spell's power
* $R(x)$ is the function that multiplies $x$ by all of the spell's resistance multipliers.
## Code
The following code can be found at `BIN/BATTLE/BTLMOVE.EMI: 0000c3c8`