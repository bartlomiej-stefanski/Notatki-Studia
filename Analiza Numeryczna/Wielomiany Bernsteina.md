
- $\text{punkt} - \text{punkt} = \text{wektor}$
- $\text{liczba}\cdot\text{wektor} = \text{wektor}$
- $\text{wektor}\pm\text{wektor} = \text{wektor}$
- $\text{punkt}\pm\text{wektor} = \text{punkt}$

- $\text{punkt} + \text{punkt} =\ ?$

Okazuje się, że to *prawie zawsze* nie ma sensu geometrycznego.
Jednak gdy wagi przy punktach będą sumować się do jedynki, to będzie...

### Kombinacja Barycentryczna

$$
\begin{align*}
&\begin{cases}
\alpha_{0},\alpha_{1},\dots,\alpha_{n} \in R : \sum\limits_{i=0}^{n}\alpha_{i} = 1\\
W_{0},W_{1},\dots,W_{n} \in \mathbb{E}^{n}
\end{cases}\\
\\
&\text{Wtedy mamy punkt: }\sum\limits_{j=0}^{n}\alpha_{j}W_{j} \in \mathbb{E}^{d}
\end{align*}
$$
Utożsamiać to będziemy z wyrażeniem:
$$
W = W_{0} + \alpha_{1}(W_{1}-W_{2}) + \alpha_{2}(W_{2}-W_{0}) + \dots + \alpha_{n}(W_{n} - W_{0})
$$
Czyli przesunięciem punktu $W_{0}$ o wektor $\alpha_{1}(W_{1}-W_{2}) + \dots + \alpha_{n}(W_{n} - W_{0})$.

### Kombinacja Wypukła

$$
\begin{align*}
&\begin{cases}
\alpha_{0},\alpha_{1}\dots,\alpha_{n}\ge0 : \sum\limits_{i=0}^{n}\alpha_{i}=1\\
W_{0},W_{1},\dots,W_{n}\in\mathbb{E}^{d}
\end{cases}\\
\\
&\text{Otoczka wypukła } W_{0},W_{1}\dots,W_{n}: \sum\limits_{j=0}^{n}\alpha_{j}W_{j}\\
&\text{Lub inaczej: } W = \sum\limits_{j=0}^{n}\alpha_{j}W_{j} \in \text{conv}\{W_{0},W_{1},\dots,W_{n}\}
\end{align*}
$$
Gdzie otoczka wypukła jest zapisana jako $\text{conv}\{W_{0},W_{1},\dots,W_{n}\}$.

## Wielomiany Bernsteina

![[Wielomiany-Bernsteina.png]]
$$
\begin{align*}
B_{k}^{n}(x) &= \binom{n}{k}x^{k}(1-x)^{n-k}
\end{align*}
$$
> Można interpretować jako szansę na $k$ sukcesów przy $n$ próbach i prawdopodobieństwie na sukces $x$.

Dla wygody przyjmijmy konwencję, że $B_{q}^{p}(x)\equiv 0 \iff q < 0 \lor q > p$.

**Obserwacje:**

- Dla dowolnego $n \in \mathbb{N}$ oraz $x \in \mathbb{R}$ zachodzi $\sum\limits_{i=0}^{n}B_{i}^{n}(x) = 1$
- $B_{k}^{n} \in \prod_{n} \setminus \prod_{n-1}$ (czyli są to wielomiany dokładnie n-tego stopnia)
- $B_{k}^{n}(x) \ge 0$ jeśli $x \in [0,1]$
- $B_{k}^{n}(x) = (1-x)B_{k}^{n-1}(x) + xB_{k-1}^{n-1}(x)$ dla $0 \le k \le n$ 
- $(B_{k}^{n}(x))' = n(B_{k-1}^{n-1}(x) - B_{k}^{n-1}(x))$  dla $0 \le k \le n$
- Wszystkie wielomiany Bernsteina stopnia n tworzą bazę $\prod_{n}$, więc $\text{lin}\{B_{0}^{n},B_{1}^{n},\dots,B_{n}^{n}\}\equiv\prod_{n}$. 
