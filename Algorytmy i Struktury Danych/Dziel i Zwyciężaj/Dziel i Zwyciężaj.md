Standardowe algorytmy *dziel i zwyciężaj* składają się z trzech zasadniczych kroków:

1. Duże dane $x$ podziel na mniejsze dane $x_{1},\dots,x_{k}$
2. Rozwiąż problem dla danych wszystkich $x_{i}$
3. Wyznacz pełne rozwiązanie dla danych $x$ na podstawie wyników dla pod problemów

Ta strategia będzie faktycznie lepsza jeżeli:

- Koszt podziału jest *mały*
- Rozwiązywanie pod-problemów jest istotnie prostsze
- Koszt łączenia małych rozwiązań w duże jest *mały*

## Złożoność Obliczeniowa Algorytmów Rekurencyjnych

Bardzo często będziemy mieć algorytmy, których złożoność będziemy mogli opisać następującym równaniem:
$$
\begin{align*}
T(n) = \begin{cases}
b &: n = 1 \\
aT(n / c) + bn &: n > 1
\end{cases}
\end{align*}
$$
Wtedy czas działania dla $a,b,c\in\mathbb{N}$ opiszemy następująco:
$$
\begin{align*}
T(n) = \begin{cases}
\Theta(n) &: a < c \\
\Theta(n \log n) &: a = c \\
\Theta(n^{\log_{c}a}) &: a > c
\end{cases}
\end{align*}
$$
**d-d:**
Niech $n = c^{k}$, czyli $k = \log_{c}n$. Wtedy stosując metodę podstawiania otrzymamy:
$$
T(n) = \frac{a^{k}bn}{c^{k}} + \frac{a^{k-1}bn}{c^{k-1}} + \dots + \frac{abn}{c} + bn = bn\sum\limits_{i=0}^{k} \left( \frac{a}{c} \right)^{i}
$$
Teraz ostatnią sumę będziemy przybliżać w zależności od $a,c$:

#### a < c

Wtedy szereg $\sum\limits_{i=0}^{\infty} \left( \frac{a}{c} \right)^{i}$ jest zbieżny, więc traktujemy go jak stałą.

#### a = c

Wtedy łatwo liczymy sumę $\sum\limits_{i=0}^{k} \left( \frac{a}{c} \right)^{i} = k+1 = \log_{c}n + 1$.

#### a > c

$$
\begin{align*}
bc^{k}\sum\limits_{i=0}^{j} \left( \frac{a}{c} \right)^{i} &= bc^{k}\frac{\left( \frac{a}{c} \right)^{k+1}-1}{\left( \frac{a}{c} \right) - 1} \\
&= b\frac{\frac{a^{k+1}}{c} - c^{k}}{\frac{a - c}{c}} \\
&= b\frac{a^{k+1} - c^{k+1}}{a-c} \\
&= \frac{ba}{a - c}a^{\log_{c}n} - \frac{cb}{a-c}c^{\log_{c}n} \\
&= O(1) \cdot a^{\log_{c}n} - O(n)
\end{align*}
$$