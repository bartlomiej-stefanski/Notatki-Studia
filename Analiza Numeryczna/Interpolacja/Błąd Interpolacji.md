## Twierdzenie

Załóżmy, że funkcja $f$, ma ciągłą $(n+1)$-szą pochodną w przedziale $[a,b]$. 
Niech $L_{n}$ oznacza wielomian interpolujący funkcję $f$ w parami różnych punktach $x_{1},x_{2},\dots,x_{n}$. Wtedy:
$$
\begin{align*}
f(x) - L_{n}(x) &= \frac{f^{(n+1)}(\xi_{x})}{(n+1)!}(x-x_{0})(x-x_{1})\dots(x-x_{n})\\
\xi_{x} \in (a, b) \land x\in [a,b]
\end{align*}
$$

### Wniosek

$$
\begin{align*}
\max_{a \le x \le b}|f(x) - L_{n}(x)| &\le \frac{\max\limits_{a\le x\le b}{|f^{(n+1)}(x)|}}{(n+1)!} \max_{a\le x \le b}|(x-x_{0})(x-x_1)\dots(x-x_{n})|
\end{align*}
$$
Nie mamy wpływu na *ułamek*, ale na wybór punktów już tak - będziemy chcieli tak dobrać ostatni iloczyn był jak najmniejszy.

## Zadanie

Rozwiązać następujący *problem optymalizacyjny*:
$$
\begin{align*}
\min_{x_{0},x_{1},\dots,x_{n}\in [a,b]} \max_{a \le x \le b} |(x-x_{0})(x-x_{1})\dots(x-x_{n})|
\end{align*}
$$

### Twierdzenie

Niech będzie $[a,b] = [-1,1]$. Wartość:
$$
\begin{align*}
M_{n} = \max_{-1 \le x \le 1} |(x-x_{0})(x-x_{1})\dots(x-x_{n})|
\end{align*}
$$
*Jest najmniejsza* $\iff x_{0}, x_{1}, \dots, x_{n}$ są miejscami zerowymi $(n+1)$-szego wielomiany Czebyszewa. 

#### Obserwacje

- $x_{k} = cos\left(\frac{2k+1}{2n+2}\pi\right)$ dla $(k = 0,1,2\dots n)$
- $M_{n} = \frac{1}{2^{n}}$
- $\exists_{M>0}\forall_{n \in \mathbb{N}}\max\limits_{-1\le x \le 1} |f^{(n+1)}(x))| \le M \implies \max\limits_{-1 \le x \le 1}|f(x) - L_{n}(x)| \le \frac{M}{(n+1)! \cdot 2^{n}} \overset{n\to\infty}{\longrightarrow} 0$ 
- Pomiędzy przedziałami $[-1, 1]$,  oraz $[a, b]$ istnieje bijekcja liniowa
