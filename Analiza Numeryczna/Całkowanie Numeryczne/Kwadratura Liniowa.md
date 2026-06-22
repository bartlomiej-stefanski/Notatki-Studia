Dla danej ciągłej funkcji $f$ *kwadraturą liniową* nazywamy wyrażenie postaci:
$$
Q_{n}(f) = \sum\limits_{k=0}^{n}A_{k}^{(n)}f(x_{k}^{(n)})
$$
Gdzie:

- $x_{k}^{(n)}$ – węzły kwadratury (parami różne)
- $A_{k}^{(n)}$ – współczynnik kwadratury

#### Zadanie

Dobrać *węzły kwadratury* i *współczynniki kwadratury* w taki sposób aby:
$$
\boxed{Q_{n}(f)\approx\int\limits_{a}^{b}f(x)dx}
$$
dla funkcji $f \in F = \{\text{dużo funkcji}\}$.

> Do dyspozycji mamy $2n+2$ parametrów (węzły i współczynniki).
> Będziemy więc chcieli, by dało się w ten sposób liczyć dokładnie wielomiany stopnia liniowo zależnego od $n$.  
> ~~taki sens był tego mniej więcej, trochę nie słuchałem~~

### Błąd Kwadratury
$$
\int\limits_{a}^{b}f(x)dx = Q_{n}(f) + \boxed{R_{n}(f)}
$$

### Rząd Kwadratury

Kwadratura liniowa $Q_{n}$ ma $\text{rząd} = r$ tylko wtedy, gdy:
1. $\forall_{w\in\prod_{r-1}}\int\limits_{a}^{b}w(x)dx = Q_{n}(w)$, czyli dla każdego $w$ mamy $R_{n}(w) = 0$
2. $\exists_{v\in\prod_{r} \setminus \prod_{r-1}}\int\limits_{a}^{b}v(x)dx \ne Q_{n}(v)$ 

> Będziemy chcieli dobierać węzły $x_{k}^{(n)}$ i współczynniki $A_{k}^{(n)}$ w taki sposób, by rząd kwadratury był największy możliwy.

#### Twierdzenie o Maksymalnym Rzędzie

$$
\text{rząd}(Q_{n}) \le 2n + 2
$$
Można pokazać, że zawsze możliwe jest wybranie wielomianu o stopniu większym niż rząd, gdzie błąd kwadratury będzie nie zerowy.

> Osiągnięcie rzędu $2n+2$ jest wykonalne, ale bardzo trudne.
