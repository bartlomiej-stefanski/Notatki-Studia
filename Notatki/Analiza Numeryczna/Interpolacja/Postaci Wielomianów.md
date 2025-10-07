### Oznaczenia

- $\prod_{n}$ – zbiór wielomianów stopnia $\le n$.

### Postać wielomianów

- Postać potęgowa (naturalna): $\prod_{n}:\ \ w(x) = \sum\limits_{k=0}^{n}a_{k} \cdot x^{k}$.
- Schemat Hornera:
    - $w_{n} = a_{n}$
    - $w_{k} = w_{k+1} \cdot x + a_{k}$
    - Będziemy obliczać wciskając wyższe potęgi "do środka"
    - Jest to algorytm numerycznie poprawny
- Postać Newtona: $w(x) = \sum\limits_{k=0}^{n}b_{k}p_{k}(x)$, gdzie:
    - $p_{0}(x) = 1$ 
    - $P_{k}(x) = (x-x_{k})p_{k-1}(x)$
    - Obserwacja: $p_{k}(x) = \prod\limits_{j=0}^{k-1}(x-x_{j})$
- Uogólniony schemat Hornera
    - $w_{n} = b_{n}$
    - $w_{k} = w_{k+1}(x-x_{k}) + b_{k}$
    - Wtedy $w_{0} = w(x)$
    - Jest to algorytm numerycznie poprawny

## Postać Czebyszewa Wielomianu

$$
\begin{align*}
\begin{cases}
T_{0}(x) \equiv 1\\
T_{1}(x) \equiv x\\
T_{k}(x) \equiv 2xT_{k-1}(x) - T_{k-2}(x)
\end{cases}
\end{align*}
$$

- $T_{k}(x) = 2^{k-1} \cdot x + \varnothing \cdot x^{k-1} + \dots$
- $T_{k}(-x) = (-1)^{k}\cdot T_{k}(x)$
- $x\in [-1,1] \implies \boxed{T_{k(x)}= cos(k\cdot arccos(x))}\boxed{FAKT}$
- **WAŻNE**: $lin\{T_{0}, T_{1}, \dots, T_{n}\} = \prod_{n}$, czyli potrafimy przedstawić każdy wielomian
- *Wszystkie* miejsca zerowe $T_{n}$ są pojedyncze, rzeczywiste i leżą w przedziale $(-1,1)$
- $|T_{n}(x)| \le 1$ dla $x \in [-1,1]$

#### Wielomian w Postaci Czebyszewa

$$
\begin{align*}
w \in \prod_{n}:&\\
&w(x) = \frac{1}{2}\cdot c_{0}  T_{0}(x) + c_{1}T_{1}(x) + \dots + c_{n}T_{n}(x)\\
&w(x) = \sum\limits_{k=0}^{n}'c_{k}T_{k}(x)\\
\sum\limits_{k=0}^{n}' y_{k} =& \frac{1}{2}y_{0} + y_{1} + \dots + y_{n}
\end{align*}
$$

---

> W jaki sposób wyznaczać wartości wielomianu podanego w postaci Czebyszewa?

Ze względów numerycznych zaleca się w tym celu wykorzystać tzm. algorytm Clenshowa.

$$
\begin{align*}
O(n) &= \begin{cases}
B_{n+2} = 0\\
B_{n+1} = 0\\
B_{k} = 2\cdot x B_{k+1} - B_{k+2} + c_{k}
\end{cases}
\end{align*}
$$

Wtedy $w(x) = \frac{B_{0} - B_{2}}{2}$.

## Postać Lagrange'a


$$
\begin{align*}
L_{n}(x) = \sum\limits_{k=0}^{n} \lambda_{k}(x)\cdot y_{k}
\end{align*}
$$
Gdzie:
$$
\begin{align*}
\lambda_{k}(x) &= \prod_{i=0}^{n}\frac{x-x_{i}}{x_{k}-x_{i}}
\end{align*}
$$

