## Multiplication by a Constant
When a variable is multiplied by a constant, the multiplication is broken down into multiplications of powers of two and additions. 
For example, let $x$ be our variable. $5x$ is written as:
$$
\begin{align*}
5x &= 4x + x\\
&=5x
\end{align*}
$$
$10x$ is written as:
$$
\begin{align*}
10x &= 2(4x + x)\\
&= 2(5x)\\
&= 10x
\end{align*}
$$
$100x$ is written as:
$$
\begin{align*}
100x &= 4((8(2x + x)) + x)\\
&= 4(8(3x) + x)\\
&= 4(24x + x)\\
&= 4(25x)\\
&= 100x
\end{align*}
$$
In the code, multiplications by power of 2 are done using left bit shifts. A left bit shift takes a number and shifts the bits to the left, adding zero at the end. It is denoted as `a << b`, where `a` is the number to be shifted, and `b` is the amount of bytes to shift.
For example, in binary, 14 is `0b00001110`. Shifting it one bit to the left gives `0b00011100`, which is 28, or 14 * 2. Shifting it two bits to the left gives `0b00111000`, which is 56, or 14 * 4.
### Instructions
#### Shift Left Logical
This instruction (`sll`) shifts the input register `$rt` by `sa` bits and stores it in `$rd`. It has the structure:

| Bits   | Description |
| ------ | ----------- |
| 000000 | `SPECIAL`   |
| 00000  | `0`         |
| xxxxx  | `rt`        |
| xxxxx  | `rd`        |
| xxxxx  | `sa`        |
| 000000 | `SLL`       |
```
sll     $rd, $rt, sa
```
##### Example
For example, the instruction
```
sll     $v0, 0x02
```
is stored as:
```
80 10 02 00
```
in both the files and the RAM, in that order. Remember that everything in the memory is little-endian. So, before converting it into bits, we read it as
```
00 02 10 80
```
Then if we convert `0x00021080` into bits, we get:
```
00000000000000100001000010000000
```
Segmenting this based on the table above:
```
000000 00000 00010 00010 00010 000000
```
If we want the instruction to right shift by three bits instead, we need to change the `sa` segment:
```
000000 00000 00010 00010 00011 000000
```
Then, to put this back into the code, we convert this back to hexadecimal:
```
00 02 10 c0
```
And then reverse the order again:
```
c0 10 02 00
```
#### Shift Left Logical Variable
This instruction (`sllv`) shifts the input register ``
### The Math
Let $b \in \mathbb{Z}^+$. By induction, we can show that $b$ can be represented as a sequence $a_0, a_1, \dots, a_n$, $a_i \in \{0,1\}$ such that:
$$
\begin{align}
b = \sum_{i=0}^{n} 2^ia_i
\end{align}
$$
The proof is trivial and left as an exercise for the readers. Left shifting by $m$ is equivalent to defining a new sequence $a'_i$ such that:
$$
\begin{align*}a_0' = 0\\
a_1' = 0\\
\vdots\\
a_{m-1}' = 0\\
a_{m}' = a_0\\
a_{m+1}' = a_1\\
\vdots\\
a_{m+n}' = a_n\\
\end{align*}
$$Therefore:
$$
b' = \sum_{i=0}^{m+n}2^i a'_i
$$
As the terms up to $a'_{m-1}$ all contain zeros, we know that the the sequence $a_i$ in $a_i'$ starts at $a_{m}$. Therefore, the smallest possible power of $2$ in the sum is $2^m$, we may factor it out

$$
b' = 2^m\sum_{i=m}^{n}2^{i-m} a'_i
$$
The sequence $a'_m, a'_{m_+1}, \dots, a'_{m+n}$ is identical to the sequence $a_0, a_1, \dots, a_n$. We may replace the sum:
$$
b' = 2^m\sum_{i=0}^n 2^ia_i
$$Notice that the right-hand side is now equivalent to
$$
b' = 2^m b
$$
Therefore, a shift of $m$ bits to the left is equivalent to multiplying $b$ with $2^m$.
## Division by a Constant
Similarly, division is easiest done with powers of 2. The operator that performs divisions (rounded down) by powers of 2 is the shift right operator. It is written as `a >> b`.
### The Math
Like before, let $b$ be a positive number and let $a_i$ be the sequence that represents $b$ in binary. If we right shift $b$ by $m$ bits, it is equivalent to defining a new sequence $a'_i$ such that:
$$
\begin{align*}
a_0' = a_{m}\\
a_1' = a_{m+1}\\
\vdots\\
a_{n-m}' = a_{n}\\
a_{n-m+1}' = 0\\
\vdots\\
a'_{n} = 0
\end{align*}
$$
We may safely ignore the terms $a_{n-m+1}',\dots,a_n'$. We then shift this left back $m$ bits, therefore obtaining a new sequence:

$$
\begin{align*}a_0'' = 0\\
a_1'' = 0\\
\vdots\\
a_{m-1}'' = 0\\
a_{m}'' = a_0' = a_m\\
a_{m+1}'' = a_1' = a_{m+1}\\
\vdots\\
a_{n}'' = a_n' = a_{n}\\
\end{align*}
$$
We take a look at the sum:
$$
b'' = \sum_{i=0}^n 2^ia''_i
$$
As the smallest power of $2$ in the sum is $2^m$, we may factor it out
$$
b'' = 2^m\sum_{i=m}^n 2^{i-m}a''_i
$$
We have shown that $b'' | 2^m$. To show that $b'' \leq b$, notice that $a_i'' \leq a_i$, for all $i = 0, 1, \dots, m-1$, after which point the two sequences are identical. By the comparison test, $b''\leq b$. 

## Modulo
Let $a\in\mathbb{Z}$, $b\in\mathbb{Z}\setminus \{0\}$. Let $q, r \in \mathbb{Z}$ such that
$$a=qb+r$$
We refer $r$ as the modulo of $a$ with respect to $b$. 
The modulo is also referred as the remainder. For example, the remainder of 23 divided by 7 is 2, as the numbers $q$ and $r$ that satisfy the equation above are $q=3$ and $r=2$. In programming, this is often denoted as `r = a % b`. For every $a$ and $b$, this number is unique. The proof is left as an exercise for the reader.
The formula above applies to both positive and negative integers, but we will focus on the positive case. To find the modulo $r = a \mod b$ of two positive integers $a \in \mathbb{Z}_0^+$, $b\in \mathbb{Z}^+$, , we use the following algorithm:
* Find $q\in\mathbb{Z}^+_0$ such that $(qb \leq a) \wedge \forall q' \in \mathbb{Z}^+_0(q' > q \Rightarrow q'b > a)$
	* In other words, find the largest multiple of $b$ smaller than $a$.
* $r$ is $a-qb$
For example, let us calculate the remainder of 250 divided by 128. The greatest multiple of 128 less than 250 is 128, therefore $q=1$. We calculate $250-1\cdot128 =122$. Therefore, the remainder is $122$.
This is easily done when $b$ is a power of 2, as the operation needed to find the largest multiple of $b$ less than $a$ can be done with left and right shifts.

