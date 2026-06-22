**Dane:**

- Ciąg liczb $d_{0},d_{1},\dots,d_{n}$ – liczby naturalne
	- Macierz $M_{i}$ jest wymiarów $d_{i-1}\times d_{i}$

**Zadanie:**
Wyznaczyć kolejność mnożenia macierzy $M_{1} \times M_{2} \times \dots \times M_{n}$ optymalną pod względem czasu.

## Motywacja

No fajnie, że mnożenie macierzy jest łączne, ale czy *musimy* z tego korzystać?
Jeżeli chcemy mnożyć efektywnie to tak.

Rozważmy macierze $M_{1},M_{2},M_{3}$ o rozmiarach $d \times 1,\ 1 \times d,\ d \times 1$. Możemy policzyć ich iloczyn na dwa sposoby:

1. $(M_{1} \times M_{2}) \times M_{3}$
	- Pierwsze mnożenie kosztować nas będzie $O(d^{2})$ obliczeń i uzyskamy macierz $d \times d$, więc drugie mnożenie również zajmie czas kwadratowy.
2. $M_{1} \times (M_{2} \times M_{3})$
	- Pierwsze mnożenie wykonamy w czasie liniowym $O(d)$. Otrzymamy w jego wyniku macierz o wielkości $1 \times 1$, więc drugie mnożenie również wykonamy liniowo.

Różnica pomiędzy czasem kwadratowym, a liniowym jest *bardzo duża*.

> Koszt mnożenia macierzy o wymiarach $a \times b$ i $b \times c$ aproksymujemy jako $a \cdot b \cdot c$ mimo tego, że istnieją szybsze algorytmy.

## Programowanie Dynamiczne

Zauważamy, że któreś z mnożeń w ciągu $M_{1} \times M_{2} \times \dots \times M_{n}$ musimy wykonać jako ostatnie. Jeżeli wybierzemy *to ostatnie* mnożenie, to wymnożenie macierzy *na lewo* i *na prawo* staje się mniejszym pod problemem – łączny koszt to operacje wymnożenia macierzy na lewo/prawo oraz *ostatnie* mnożenie macierzy. 

Na podstawie tej obserwacji możemy zbudować rozwiązanie dynamiczne:
$$
\begin{align*}
dp[i][j] &= \begin{cases}
0 &: i = j \\
\min_{k\in\{i, \dots,j-1\}}(dp[i][k] + dp[k+1][j] + d[i-1]d[k]d[j]) &: \text{w p.p.}
\end{cases} \\
dp[i][j] &= \text{minimalny koszt mnożenia macierzy } M_{i} \times \dots \times M_{j}
\end{align*}
$$
> Taka *struktura* rozwiązań problemów programowaniem dynamicznym jest dosyć częsta!

### Złożoność Czasowa

Mamy do wyznaczania kwadratowo-wiele wartości tablicy $dp$ oraz każde wyznaczenie zajmuje czas $O(n)$, stąd cały algorytm wykonamy w czasie $O(n^{3})$.

### Odtworzenie Rozwiązania

uh oh
Mieliśmy wyznaczyć kolejność, ale wyznaczyliśmy minimalną liczbę mnożeń.
Jeżeli w każdym polu $dp[i][j]$ zapamiętamy dla jakiego $k$ podział jest najlepszy, to będzie łatwo odtworzyć.
Jeżeli nie, to czeka nas kwadratowe przetwarzanie.