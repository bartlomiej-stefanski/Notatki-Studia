To [[Kwadratura Interpolacyjna|Liniowa Kwadratura Interpolacyjna]] dla węzłów równo odległych w przedziale całkowania.
$$
\begin{align*}
x_{k}^{(n)} &= a + kh\\
h &= \frac{b-a}{n}
\end{align*}
$$
Pozwala to na pewne uproszczenia.

1. Postać Lagrange'a wielomianu interpolacyjnego upraszcza się do węzłów równo odległych
2. $A_{k}^{(n)} = \frac{(-1)^{n-k}h}{k!(n-k)!}\cdot\int\limits_{0}^{n}\prod\limits_{j=0,j\ne k}^{n}(t - j)dt$
3. $A_{k}^{(n)} = A_{n-k}^{(n)}$

## Błąd Kwadratury Newtona-Cotesa

$$
\begin{align*}
R_{n}^{NC} &= \begin{cases}
\frac{f^{(n+1)}(\xi)}{(n+1)!}\int\limits_{a}^{b}(x-x_{0}^{(n)})(x-x_{1}^{(n)})\dots(x-x_{n}^{(n)})dx &: (n=1,3,5,\dots)\\
\frac{f^{(n+1)}(\xi)}{(n+2)!}\int\limits_{a}^{b}(x-x_{0}^{(n)})(x-x_{1}^{(n)})\dots(x-x_{n}^{(n)})dx &: (n=2,4,6,\dots)
\end{cases}
\end{align*}
$$

> To jest najgorsza możliwa kwadratura pod względem rzędu przybliżenia :(

$$
\begin{align*}
\text{rząd}(Q_{n}^{NC}) &= \begin{cases}
n+2 : 2\mid n\\
n+1 : 2\nmid n
\end{cases}
\end{align*}
$$
Rozważmy kwadraturę *Newtona-Cotesa* dla $n=1,n=2$.
Dla $n\ge7$ nie zaleca się już korzystania z tej metody.

## Wzór Trapezów

> Czyli $n = 1$

$$
\begin{align*}
Q_{1}^{NC}(f) &= \frac{b-a}{2}(f(a) + f(b))\\
R_{1}^{NC}(f) &= -\frac{(b-a)^{3}}{12}f''(\xi), &\xi\in(a,b), f\in C^{2}[a,b]
\end{align*}
$$

Intuicyjnie po prostu rysujemy trapezy o tak samo długiej podstawie.

## Wzór Simpsona

> Czyli $n=2$

$$
\begin{align*}
Q_{2}^{NC}(f) &= \frac{b-a}{6}\left[f(a)+4f\left(\frac{a+b}{2}\right)+ f(b)\right]\\
R_{2}^{NC}(f) &= -\frac{1}{90}\left(\frac{b-a}{2}\right)^{5}f^{(4)}(\xi), &\xi \in(a,b), f\in C^{4}[a,b]
\end{align*}
$$



