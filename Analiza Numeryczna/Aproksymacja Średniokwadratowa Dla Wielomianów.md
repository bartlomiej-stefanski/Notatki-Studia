Przyjmijmy, że modelem jest *zbiór wielomianów* stopnia mniejszego niż $m$.
Wtedy $\mathscr{X} = \prod_{m}$

**Zadanie:**
Dla ustalonej funkcji $f$ oraz $x_{0}<x_{1}<\dots<x_{N}, N \ge m$ znaleźć $\omega_{m}^{*}\in\prod_{m}$:
$$
\begin{align*}
||f-\omega_{m}^{*}||_{2} &= \min_{\omega\in\prod_{m}}||f-\omega||_{2}=\min_{\omega\in\prod_{m}}\sqrt{\sum\limits_{k=0}^{N}(f(x_{k})- \omega_{m}(x_{k}))^{2}}
\end{align*}
$$

Takie coś potrafimy rozwiązać bez jakiegoś większego myślenia w czasie $O(Nm^{2}+m^{3})$.
To jest *dużo*, a dodatkowo w tym szczególnym przypadku otrzymamy [[Macierz Vandermonde]] której nie będziemy potrafili rozwiązać [[Algorytmy Numerycznie Poprawne|Algorytmem Numerycznie Poprawnym]].

## Lepszy Algorytm

Wykorzystamy [[Aproksymacja Średniokwadratowa#Alternatywny Sposób Liczenia|Alternatywny Sposób Liczenia]] dla ortogonalnej bazy przestrzeni $\prod_{m}$.
Ortogonalność bazy sprawi, że iloczyn skalarny dwóch różnych elementów będzie zerowy, stąd w macierzy nie-zerowe wartości będą tylko na przekątnej – mamy rozwiązanie.

### Ortogonalna Baza Przestrzeni Wielomianów

Układ funkcji $f_{0},f_{1},\dots,f_{n}$ nazywamy *układem ortogonalnym* jeśli:
$$
<f_{i},f_{j}> =\begin{cases}
0 &: i\ne j \\
y \ne 0 &: i=j
\end{cases}
$$
Dla wybranego iloczynu skalarnego tworzyć on będzie bazę przestrzeni.
Nasze funkcje to wielomiany, więc będą tworzyć przestrzeń $\prod_{m}$ oraz każde $f_{i}$ będzie innego stopnia.

**Zadanie:**
Dana jest przestrzeń liniowa $lin\{g_{0},g_{1}\dots,g_{n}\} = G$, Jak skonstruować *bazę ortogonalną*?

> Może algorytm Grama-Schmidta?

Nie, bo zbyt drogi – wymaga kwadratowej ilości iloczynów skalarnych i jest numerycznie niepoprawny.

**Rozwiązanie:**
Możemy zortonormalizować bazę standardową $\prod_{m}:1,x,x^{2},\dots,x^{m}$, ale użyjemy algorytmu innego niż Grama-Schmidta – uwiniemy się w $O(mN)$.

#### Wyznaczanie Bazy Ortogonalnej Wielomianów

Poniższe twierdzenie pokazuje jak wyznaczyć ciąg wielomianów ortogonalnych $P_{0},P_{1},\dots,P_{m}$, gdzie $m \le N$ względem $<\cdot,\cdot>_{N}$ w czasie $O(mN)$:
$$
\begin{align*}
&\begin{cases}
P_{0}(x) \equiv1 \\
P_{1}(x) = x - c_{1} \\
P_{k}(x) = (x-c_{k})P_{k-1}(x) - d_{k}P_{k-2}(x)
\end{cases}\\
\\
\text{Gdzie:}\\
c_{k}&= \frac{<xP_{k-1}, P_{k-1}>}{<P_{k-1},P_{k-1}>}\tag{k = 1,2,...}\\
d_{k}&= \frac{<P_{k-1},P_{k-1}>}{<P_{k-2},P_{k-2}>}\tag{k = 2,3,...}
\end{align*}
$$

Wielomiany $P_{0},P_{1},\dots,P_{m}$ będziemy wyznaczać w kolejności.
Aby policzyć wartość $P_{0}(x),P_{1}(x),\dots,P_{m}(x)$ dla ustalonego $x$ musimy wcześniej znać wartości $c_{1},c_{2},\dots,c_{m}$ i $d_{2},d_{3},\dots,d_{m}$.
Okaże się, że nadal będziemy w stanie wykonać te obliczenia w $O(mN)$.

#### Jak To Liczyć?

Kombinację liniową *wielomianów ortogonalnych* zaleca się wyznaczać przy pomocy  [[Algorytm Clenshawa|Algorytmu Clenshawa]] – tak jak w przypadku [[Postaci Wielomianów#Postać Czebyszewa Wielomianu|Wielomianów Czebyszewa]].

Stąd dla raz policzonych wartości $c_{i}$ i $d_{i}$ będziemy potrafili wyznaczyć wartość $\sum\limits_{k=0}^{N}\alpha_{0}P_{k}(x)$ w czasie liniowym.

### Twierdzenie

> Które wynika z tego co co zapisaliśmy powyżej

$$
\omega_{m}^{*}(x) = \sum\limits_{k=0}^{N}\alpha_{k}P_{k}(x)
$$
Gdzie $P_{0},P_{1},\dots,P_{N}$ są wielomianami ortogonalnymi względem $<\cdot,\cdot>_{N}$
Oraz współczynniki $\alpha_{i}$ definiujemy jako:
$$
\alpha_{i} = \frac{<f,P_{i}>}{<P_{i},P_{i}>} = \frac{\sum\limits_{k=0}^{N}f(x_{k})P_{i}(x_{k})}{\sum\limits_{k=0}^{N}P_{i}(x_{k})^{2}}
$$
Czyli wystarczy znać wartości wielomianów ortogonalnych w punktach $x_{i}$.

**Uwaga:**
- Będziemy chcieli skończyć dodawać kolejne wektory ortogonalne, gdy ich współczynniki $\alpha_{i}$ będą bliskie zera.
- $||f-w_{n}^{*}||_{2} = \sqrt{||f||_{2}-\sum\limits_{k=0}^{m}\frac{(<f,P_{k}>)^{2}}{<P_{k},P_{k}>}}$ jest wzorem na błąd aproksymacji.
	- Stąd zwiększenie stopnia wielomianu nie pogorszy aproksymacji.