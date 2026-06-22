---
tags:
  - MDM-checklist
---
> ...czyli *sztuka* wyznaczania zwartej postaci funkcji.

## Zależność Rekurencyjna
### Szereg Potęgowy

$$\begin{align*}
S_{n} &= 1 + q + q^{2} + q^{3} + \dots + q^{n}\\
S_{n+1} &= 1 + qS_{n}\\
S_{n} &= \frac{1-q^{n+1}}{1-q}
\end{align*}$$
Można rozwiązać korzystając z [[Anihilatory|anihilatorów]]:
$$\begin{align*}
S_{n+1} - 1 - qS_{n} &=0\\
(E-q)(E-1)\langle S_{n}\rangle &= \langle0\rangle\\
S_{n} &= A + Bq^{n}\\
\\
\begin{cases}
S_{0} = 1 = A + B\\
S_{1} = 1 + q = A + qB
\end{cases}&\implies q=B(q-1) \implies B = \frac{q}{q-1}\\
1 &= A + \frac{q}{q-1}\\
1-\frac{q}{q-1} &= A\\
\frac{q-1}{q-1}-\frac{q}{q-1} &= A\\
\frac{-1}{q-1} &= A
\end{align*}$$
## Pochodna

$$T_{n} = q + 2q^{2} + 3q^{3} + \dots + nq^{n}$$
Zauważamy, że ciąg ten bardzo podobny do pochodnej ciągu $S_{n}$:
$$\begin{align*}
S_{n}(q) &= 1 + q + q^{2} + q^{3} + \dots + q^{n}\\
S_{n}'(q) &= 1 + 2q + 3q^{2} + \dots + nq^{n-1}\\
q \cdot S_{n}'(q) &= q + 2q^{2} + \dots +nq^{n}\\
\\
T_{n}(q) = q\cdot S_{n}(q) &= q\cdot \left(\frac{1-q^{n+1}}{1-q}\right)'\\
&= q\cdot \frac{(n+1)q^{n}(1-q) + 1-q^{n+1}}{(1-q)^{2}}\\
&= \frac{q - (n+1)q^{n+1} + nq^{n+2}}{(q-1)^{2}}
\end{align*}$$

## Potęgi Ubywające

$$\begin{align*}
(n+1)^{\underline{k+1}} &= (n+1)n^{\underline{k}}\\
n^{\underline{k+1}} &= n^{\underline{k}}(n-k)\\
\\
(n+1)^{\underline{k+1}}-n^{\underline{k+1}} &= n^{\underline{k}}(n+1 - n + k)\\
&= n^{\underline{k}}(k+1)\\
n^{\underline{k}} &= \frac{(n+1)^{\underline{k+1}}}{k+1} - \frac{n^{\underline{k+1}}}{k+1}\\
\\
\sum\limits_{i=a}^{b}i^{\underline{k}} &= \frac{(b+1)^{\underline{k+1}} - a^{\underline{k+1}}}{k+1}
\end{align*}$$

### Przykład

$$\begin{align*}
\sum\limits_{n=1}^{N}n(n-1) &= \sum\limits_{n=1}^{N}n^{\underline{2}} = \frac{(N+1)(N)(N-1) - 0}{2+1}
\end{align*}$$

### Potęgi Ujemne

$$\begin{align*}
n^{\underline{k}} &= \frac{n^{\underline{k+1}}}{n-k}\\
n^{\underline{0}} &= 1\\
n^{\underline{-1}} &= \frac{1}{n+1}\\
n^{\underline{-2}} &= \frac{\frac{1}{n+1}}{n+2} = \frac{1}{(n+1)(n+2)}
\end{align*}$$

