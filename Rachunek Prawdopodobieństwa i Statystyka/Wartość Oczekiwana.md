*Wartością oczekiwaną* [[Zmienna Losowa|zmiennej losowej]] $X$ nazywamy $EX = E(X)$ równe odpowiednio:

- $\sum\limits_{i}x_{i}p_{i}$ dla dyskretnej zmiennej
- $\int_{\mathbb{R}}xf(x)dx$ dla ciągłej zmiennej

> Intuicyjnie jest to *spodziewana* wartość zmiennej $X$.

## Własności

### Liniowa Transformacja Zmiennej

$$
E(aX + b) = aE(X) + b
$$
**d-d:**  
$$
\begin{align*}
E(aX + b) &= \int_{\mathbb{R}}(ax + b)f(x)dx\\
&= a\int_{\mathbb{R}}xf(x)dx + b\int_{\mathbb{R}}f(x)dx\\
&= aE(x) + b
\end{align*}
$$

### Iloczyn Zmiennych Niezależnych

Dla niezależnych $X,Y$ zachodzi $E(XY) = E(X)\cdot E(Y)$.

#TODO 

### Alternatywny Wzór Dla Dziedziny Naturalnej

Jeżeli dziedziną $X$ są liczby $\{1,\dots,n\}$, to:
$$
E(X) = \sum\limits_{1}^{n}P(X \ge i)
$$
**d-d:**  
Zauważmy, że $P(X = k)$ weźmiemy dla każdego $k \ge i \in \mathbb{N}$, których jest łącznie $k$.   Odpowiada to więc uwzględnieniu $k \cdot P(X = k)$, więc wszystkich składników jest tyle co potrzeba.