Zacznijmy od motywacji za tym wszystkim...

| Reprezentacja Wielomianu    | Dodawania Wielomianów | Mnożenie Wielomianów |
| --------------------------- | --------------------- | -------------------- |
| Tablica Współczynników      | $O(n)$                | $O(n^{2})$           |
| Tablica Wartości w Punktach | $O(n^{2})$            | $O(n)$               |

By wykonywać operacje *szybko* będziemy chcieli więc przenosić się pomiędzy reprezentacjami *o ile się da dosyć szybko* – docelowo w czasie $O(n\log n)$.

### Naiwne Zamiany Reprezentacji

#### Współczynniki -> Wartości w Punktach

Wystarczy obliczyć (np. schematem Hornera) wartości wielomianu o stopniu $n-1$ w $n$ punktach. To jest do zrobienia w czasie $O(n^{2})$.

#### Wartości w Punktach -> Współczynniki

Korzystamy z [[Interpolacja Wielomianowa|interpolacji]], która pozwala jednoznacznie odtworzyć wielomian przechodzący przez dane punkty w czasie $O(n^{2})$.

## Pierwiastki z Jedności

Okaże się, że bardzo przydadzą się pierwiastki z jedności (liczb zespolonych).
Zbiór pierwiastków $n$-tego stopnia z jedności to:
$$
\{w_{n}^{k} = e^{\frac{2\pi \cdot ik}{n}} : k\in\{0,\dots,n-1\}\}
$$
lub izomorficznie:
$$
\left\{ w_{n}^{k} = \cos\left( \frac{2k\pi}{n} \right) + i\sin\left( \frac{2k\pi}{n} \right) : k\in\{0,\dots,n-1\} \right\}
$$
> Zbiory te tworzą *grupę* izomorficzną z $(\mathbb{Z}_{n}, +)$.

**Fakt:**
Zbiór $\{(w_{n}^{i})^{2} : i \in \{0,\dots,n-1\}\}$ jest równy $\left\{ w_{\frac{n}{2}}^{i} : i \in \left\{ 0,\dots, \frac{n}{2}-1 \right\} \right\}$, czyli zbiorowi o połowę mniejszemu.

#### Pierwotne Pierwiastki z Jedynki

Pierwotnymi pierwiastkami nazywamy te spośród pierwiastków $w_{n}^{k}$, które są generatorami grupy. Po ludzku oznacza to, że z pierwiastka pierwotnego można uzyskać wszystkie inne pierwiastki biorąc go do odpowiedniej potęgi.

**Fakt:**
$w_{n}^{1}$ jest pierwiastkiem pierwotnym dla każdego $n$.
**d-d:**
By uzyskać $w_{n}^{k}$ wystarczy wziąć $w_{n}^{1}$ do $k$-tej potęgi.

**Twierdzenie:**
Pierwiastków pierwotnych dla $n$ jest $\phi(n)$ wiele, gdzie $\phi$ to [[Liczby Względnie Pierwsze – Funkcja Eulera|Funkcja Eulera]].
**d-d:**
Poza zakresem wykładu, ale można się domyślić.

## Tablica Współczynników -> Wartości w Punktach

Na podstawie wielomianu:
$$
A(x) = a_{0} + a_{1} + a_{2}x^{2} + \dots + a_{n-1}x^{n-1}
$$
Tworzymy wielomiany:

- $A^{[p]}(z) = a_{0} + a_{2}z + a_{4}z^{2} + \dots + a_{n-2}z^{(n-2)/2}$
- $A^{[n]}(z) = a_{1} + a_{3}z + a_{5}z^{2} + \dots + a_{n-1}^{(n-2)/2}$

Wtedy $A(x) = A^{[p]}(x^{2}) + xA^{[n]}(x^{2})$.

### Jakie Punkty Policzymy?

- $A(w_{n}^{0}) = A^{[p]}((w_{n}^{0})^{2}) + w_{n}^{0}A^{[n]}((w_{n}^{0})^{2})$
- $A(w_{n}^{1}) = A^{[p]}((w_{n}^{1})^{2}) + w_{n}^{1}A^{[n]}((w_{n}^{1})^{2})$
- $\vdots$
- $A(w_{n}^{n-1}) = A^{[p]}((w_{n}^{n-1})^{2}) + w_{n}^{n-1}A^{[n]}((w_{n}^{n-1})^{2})$

Wybór tych punktów pozwoli na zastosowanie techniki [[Dziel i Zwyciężaj]]. Zauważamy bowiem, że wartości $A^{[p]},A^{[n]}$ wystarczy policzyć dla zbioru kwadratów $\{(w_{n}^{i})^{2} : i \in \{0,\dots,n-1\}\}$, który jest o połowę mniejszy niż oryginalny zbiór!
Dostajemy więc do rozwiązania dwa o połowę mniejsze problemy, z których potrafimy w czasie liniowym odtworzyć rozwiązanie, wszystko działa!

#### Algorytm

```
A[0..n-1] // kolejne współczynniki wielomianu

def FFT(A[0..n-1]):
	if n == 1:
		return a // jedno-elementowa tablica
	
	w[0..n-1] = 'i-te pierwiastki z jedynki'
	W = 1
	
	Ap[0..n/2 - 1] = 'A[i] dla parzystych i'
	An[0..n/2 - 1] = 'A[i] dla nieparzystych i'
	
	Yp = FFT(Ap)
	Yn = FFT(An)
	
	Y[0..n-1] // przestrzeń na wyniki y[i] = A(w[i])
	for k in 0..n/2 - 1:
		Y[k] = Yp[k] + w * Yn[k]
		
		// Dla n parzystych pierwiastki są symetryczne wzg. osi OX
		Y[k + n/2] = Yp[k] - w * Yn[k]
		w = w * w[k]
	
	return Y
```

#### Analiza Złożoności

Czas potrzebny na wykonanie algorytmu dla wielomianu $n$-tego stopnia opisuje równanie:
$$
T(n) = 2T\left( \frac{n}{2} \right) + \Theta(n) \implies T(n) = O(n\log n)
$$

## Wartości w Punktach -> Tablica Współczynników

Najpierw zauważmy, że to co zrobiliśmy w poprzednim punkcie odpowiada mnożeniu macierzy:
$$
\begin{align*}
\begin{bmatrix}
1 & (w_{n}^{0})^{1} & (w_{n}^{0})^{2} & \dots &(w_{n}^{0})^{n-1}  \\
1 & (w_{n}^{1})^{1} & (w_{n}^{1})^{2} & \dots &(w_{n}^{1})^{n-1} \\
\vdots & \vdots & \vdots & \ddots & \vdots\\
1 & (w_{n}^{n-1})^{1} & (w_{n}^{n-1})^{2} & \dots &(w_{n}^{n-1})^{n-1}
\end{bmatrix} \begin{bmatrix}
a_{0} \\ a_{1} \\ \vdots \\ a_{n-1}
\end{bmatrix} 
&= 
\begin{bmatrix}
y_{0} \\ y_{1} \\ \vdots \\ y_{n-1}
\end{bmatrix} \\
V_{n}A &= Y
\end{align*}
$$
*Jak widać* macierz $V_{n}$ jest macierzą [[Macierz Vandermonde|Voldemorta]], której cechą jest *trywialna* odwrotność:
$$
\begin{align*}
V_{n}^{-1} = \frac{1}{n}\begin{bmatrix}
1 & (w_{n}^{0})^{-1} & (w_{n}^{0})^{-2} & \dots & (w_{n}^{0})^{-(n-1)} \\
1 & (w_{n}^{1})^{-1} & (w_{n}^{1})^{-2} & \dots & (w_{n}^{1})^{-(n-1)} \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
1 & (w_{n}^{n-1})^{-1} & (w_{n}^{n-1})^{-2} & \dots & (w_{n}^{n-1})^{-(n-1)}
\end{bmatrix}
\end{align*}
$$

Stąd możemy wyciągnąć wzór na poszczególne współczynniki:
$$
\begin{align*}
a_{i} &= \frac{1}{n}\sum\limits_{j=0}^{n-1}y_{j}w_{n}^{-ij} \\
y_{i} &= \sum\limits_{j=0}^{n-1}a_{j}w_{n}^{ij}
\end{align*}
$$
Widzimy, że wzory są praktycznie identyczne. Wnioskujemy więc, że do obliczania wyznaczników można użyć tej samej funkcji co do wyznaczania wartości w punktach. Musimy jedynie:

- Użyć odwrotności pierwiastków z jedności
	- To nie jest trudne, bo $w_{n}^{-k} = w_{n}^{n-k}$
- Na koniec podzielić wyniki przez $n$
