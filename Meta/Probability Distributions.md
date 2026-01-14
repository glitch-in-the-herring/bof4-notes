## Definition
A continuous probability function is a function $f(y)$ such that:
* $\displaystyle\int_{-\infty}^\infty f(y)\;dy=1$ 
* $f(y) \geq 0, y \in (-\infty, \infty)$  
The limits $(-\infty, \infty)$ may be replaced some other appropriate limit. Alternatively, for a probability function that is only valid in an interval $[a,b]$, the value of the function at the intervals $(-\infty,a)$ and $(b,\infty)$ may be defined to be zero.
## Expected Value
The expected value is an extension of the concept of "averages" into the continuous world. Let $Y$ be a random variable with the probability function $f_Y(y)$. Its variance is defined as:
$$
E(Y) = \int_{-\infty}^\infty f_Y(y)y\; dy
$$
If we want to take the expected value of a function of a random variable we use:
$$
E(g(Y)) = \int_{-\infty}^\infty f_Y(y)g(y)\; dy
$$
### Applications
*This will be updated when I find how the Holy Mantle works in IV*
*...and the actual distribution of the random number generator.*
Imagine that normally, the game determines the number of steps required before a random battle by rolling `random(0, 100)`. For now let's assume that the range of this function is the real number interval $[0,100]$ and that the probability distribution of the random generator is uniform. That means our probability function will be
$$
f_Y(y) = 
\begin{cases}
\frac{1}{100} & 0 \leq y \leq 100\\
0 & \mathrm{otherwise}
\end{cases}
$$
The expected value of the rolls is:
$$
\begin{align*}
E(Y) = \mu &=   \int_{0}^{100} f_Y(y)y\; dy\\
&= \int_{0}^{100} \frac{y\; dy}{100} \\
&= 50
\end{align*}
$$
Which is more or less in line with our intuition of "average": as we roll more and more, the average of the rolls will eventually tend to 50. 
Let's imagine that the Holy Mantle is an accessory that, when equipped, takes this threshold and doubles it. So now, what's the "average" threshold? 
Let's use the equation for functions of the random variable above, by letting $g(Y)=2Y$:
$$
\begin{align*}
E(g(Y)) &= \int_{0}^{100} f_Y(y)g(y)\; dy\\
&= \int_{0}^{100} \frac{2y \; dy}{100}\\
&= 100\\
\end{align*}
$$
So it doubles the average threshold, but that doesn't tell us everything. No we turn to the...
## Variance
The variance measures how far away values are spread out from the expected value. A probability distribution that has little variance means that, if you use it in a random number generator, you're likely to land really close to the expected value. If the variance is large, you'll likely end up really far from the expected value. Let $Y$ be a random variable with the probability function $f_Y(y)$. Its variance is defined as:
$$
\begin{align*}
\mathrm{Var}(Y) = E[(Y-\mu)^2] = \int_{-\infty}^\infty f_Y(y)(y-\mu)^2\; dy\\
\end{align*}
$$
Intuitively, you can think of it as finding the expected value of the squared deviation of the random variable $Y$ from the mean $\mu$.
If we take the variance of the random variable multiplied by a constant:
$$
\mathrm{Var}(aY) = a^2\mathrm{Var}(Y)
$$
### Applications
We've seen the expected value of our random number generator, but what about its variance? For uniform distributions, as they are *uniform*, they generally have large variances:
$$
\begin{align*}
\mathrm{Var}(Y) &= \int_{0}^{100} f_Y(y)(y-\mu)^2\; dy\\
&= \int_{0}^{100} \frac{(y-50)^2\; dy}{100}\\
&= 833.333...
\end{align*}
$$
What happens to the random variable when you multiply the random variable by 2? Well, we can use the equation for that:

$$
\begin{align*}
\mathrm{Var}(2Y) &= 2^2\mathrm{Var}(Y)\\
&= 4\cdot 833.333...\\
&= 1666.6667...
\end{align*}
$$
That means the Holy Mantle increases the variance.
## Commonly Used Distributions
### Uniform
The uniform distribution is given by the following pdf:
$$
f_Y(y)=\begin{cases}
0&y<a\\
\frac{1}{b-a}&a \leq y \leq b\\
0 & y > b
\end{cases}
$$
Where $a$ and $b$ are the minimum and maximum values respectively.
### Normal
The normal distribution is given by the following pdf:
$$
f_Y(y) = \frac{1}{\sqrt{2\pi}\sigma}\exp\left(-\frac{1}{2}\left(\frac{y-\mu}{\sigma}\right)^2\right)
$$
Where $\sigma$ is the standard deviation and $\mu$ is the mean.