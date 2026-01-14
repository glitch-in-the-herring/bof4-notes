## Primus
$$
d = \max\left(0, \delta- DEF_{D}\right)
$$
$$
F_{INT} = \begin{cases}
100-\frac{INT_{D}}{5}&100-\frac{INT_{D}}{5} \geq50\\
50 & 100-\frac{INT_{D}}{5} < 50
\end{cases}
$$
$$
\alpha = \left\lfloor\frac{F_{INT}}{100}\cdot\frac{10000P(INT_{A} + 100)}{100}\right\rfloor
$$
$$
\beta = \begin{cases}
\alpha\left(100-\left\lfloor\frac{\alpha}{5000}\right\rfloor\right) & 100 - \left\lfloor\frac{\alpha}{5000}\right\rfloor \geq 80\\
80\alpha & 100 - \left\lfloor\frac{\alpha}{5000}\right\rfloor < 80
\end{cases}
$$
$$
\gamma =\left\lfloor\frac{1}{100}\cdot \frac{\beta\mathrm{random}(90,100)}{100}\right\rfloor
$$$$
\delta = \left\lfloor\left\lfloor\frac{100\gamma}{100}\cdot R_\mathrm{magic}\right\rfloor\cdot\frac{1}{100000}\right\rfloor
$$
* $P$ = spell power, normally 15 for Primus