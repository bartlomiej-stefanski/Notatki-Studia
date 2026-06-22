$$
\int\limits_{a}^{b}f(x)dx = \sum\limits_{k=0}^{n-1}\int\limits_{x_{k}}^{x_{k+1}}f(x)dx
$$
Będziemy chcieli podzielić przedział całkowania na pod przedziały, w których funkcja niewiele się zmienia, a następnie przybliżyć wartości całek w kolejnych pod przedziałach *prostą* [[Kwadratura Liniowa|kwadraturą liniową]].

## Złożony Wzór Trapezów

Dla $n+1$ punktów (indeksowanych od $0$) zdefiniujmy $x_{k}= a+kh$ i $h = \frac{b-a}{n}$.
![[Złożony_wzór_trapezów.png]]
$$
\begin{align*}
\int\limits_{x_{k}}^{x_{k+1}}f(x)dx &= \frac{h}{2}(f(x_{k}) + f(x_{k+1})) - \frac{h^{3}}{12}f''(\xi_{k}) & (\xi_{n}\in(x_{k},x_{k+1}))
\end{align*}
$$
Stąd:
$$
\begin{align*}
\int\limits_{a}^{b}f(x)dx &= \sum\limits_{k=0}^{n-1}\int\limits_{x_{k}}^{x_{k+1}}f(x)dx = T_{n}(f) + R^{T}_{n}(f)
\end{align*}
$$

- $T_{n}(f)$ – Złożony wzór trapezów
	- $T_{n}(f) = h {\sum\limits_{k=0}^{n}}'' f(x_{k})$
- $R_{n}^{T}(f)$ – błąd złożonego wzoru trapezów
	- $R_{n}^{T}(f) = -\frac{h^{3}}{12}\boxed{\sum\limits_{k=0}^{n-1}f''(\xi)} \overset{\boxed{!}}{=}-n\frac{h^{3}}{12}f''(\beta) = O(\frac{1}{n^{2}})$ jeśli $f\in C^{2}[a,b]$ i $\beta\in(a,b)$ 

> Dziwna suma: ${\sum\limits_{i=0}^{n}}'' x_{i} = \frac{x_{0}}{2} + x_{1} + \dots + x_{n-1} + \frac{x_{n}}{2}$

#### Twierdzenie
$$
\begin{align*}
f\in C[a,b] : \lim_{n\to\infty}T_{n}(f) = \int\limits_{a}^{b}f(x)dx
\end{align*}
$$
> Udowadniać z definicji całki, a nie poprzez założenie tezy.

## Złożony Wzór Simpsona

Zrobimy to samo co dla trapezów, tylko teraz dla każdego przedziału potrzebujemy trzech punktów, a nie dwóch.
Oznaczmy więc $n = 2m, m\in\mathbb{N}$, $x_{k}= a+kh$ oraz $h = \frac{b-a}{n}$ .

$$
\begin{align*}
(f\in C^{4}[a,b]) &: \int\limits_{x_{2k}}^{x_{k+2}}f(x)dx = \frac {h}{3}(f(x_{2k}) + 4f(x_{2k+1}) + f(x_{2k+2})) - \frac{h^{5}}{90}f^{(4)}(\alpha_{k}) 
\end{align*}
$$
Stąd:
$$
\begin{align*}
\int\limits_{a}^{b}f(x)dx &= \sum\limits_{k=0}^{n-2}\int\limits_{x_{2k}}^{x_{2x+2}}f(x)dx = S_{n}(f) + R_{n}^{S}(f)
\end{align*}
$$

- $S_{n}(f)$ – Złożony wzór Simpsona
	- $S_{n}(f) = \frac{h}{3}\left(2{\sum\limits_{k=0}^{m}}''f\left(x_{2k}\right) + 4\sum\limits_{k=1}^{m}f(2_{2k-1})\right)$
- $R_{n}^{S}(f)$ Błąd złożenia wzoru Simpsona
	- $R_{n}^{S}(f) \overset{\boxed{!}}{=} (a-b)\frac{h^{4}}{180}f^{(4)}(\gamma) = O(\frac{1}{n^{4}})$ jeśli $f\in C^{4}[a,b]$ i $\gamma\in[a,b]$

#### Uwaga

| Liczba próbek | Cyfry Dokładne $T_{2^{n}}$ | Cyfry Dokładne $S_{2^{n}}$ |
| ------------- | -------------------------- | -------------------------- |
| 10            | 7                          | 14                         |
| 11            | 8                          | 16                         |
| 12            | 8                          | 17                         |
| 13            | 9                          | 18                         |
| 14            | 10                         | 18                         |
| 15            | 10                         | 19                         |

Z niedokładnych cyfr przybliżenia będziemy potrafili wyciągnąć dodatkowe informacje:
$$
\begin{align*}
S_{n}(f) &= \frac{4T_{n}(f) - T_{m}(f)}{4 - 1} & (n=2m)
\end{align*}
$$
