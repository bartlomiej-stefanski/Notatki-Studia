**Dane:**
Sieć przełączników, każdy z dwoma wejściami i wyjściami. Przełącznik może nie zmienić wartości lub zamienić je miejscami.

**Zadanie:**
Skonstruować sieć przełączników umożliwiającą otrzymanie dowolnej permutacji.

**Kryteria Oceny Rozwiązania:**

- Liczba niezbędnych przełączników
- Głębokość sieci – maksymalna liczba przełączników przez jakie być może trzeba przejść na drodze od wejścia do wyjścia

## Dolne Ograniczenia

### Głębokość Sieci

Jeżeli chcemy mieć możliwość otrzymania dowolnej permutacji, to konieczna jest możliwość przesunięcia pewnego (np. pierwszego) elementu na dowolne inne miejsce. 
Wtedy siecią o minimalnej głębokości zapewniającą taką możliwość będzie drzewo binarne o $n$ liściach, każdy podpięty do innego wyjścia. Minimalna głębokość takiego drzewa to $\log n$.
Stąd ograniczenie na głębokość to: $\Omega(\log n)$.

### Liczba Przełączników

Możliwych permutacji jest $n!$.
*Spodziewamy się*, że by otrzymać inną permutację trzeba zmienić stan co najmniej jednego przełącznika, stąd minimalna liczba przełączników jest większa niż $\log_{2}(n!)$.
Z tego dostajemy ograniczenie na liczbę przełączników: $\Omega(n \log n)$.
$$
\log_{2}(n!) = \sum\limits_{k=1}^{n}\log_{2}(k) \ge \sum\limits_{k=\left\lceil  \frac{n}{2}  \right\rceil }^{n}\log_{2}(k) \ge \left( n - \frac{n}{2} \right)(\log_{2}n - 1) = \Omega (n \log n)
$$

## Konstrukcja Benetta Walksmana

> Poniższa konstrukcja działa tylko dla $n = 2^{k}$, ale nie przejmujemy się tym :D

![[Siec-przelacznikow.jpg]]
> Rysunek jest dla sieci $8$ elementowej, ale można się domyślić *generalnej konstrukcji*.

Wykorzystamy strategię dziel i zwyciężaj – obserwujemy, że utworzenie sieci generującej permutacje dla połowy wejść jest prostsze.

By skonstruować sieć dla $2^{k}$ wejść użyjemy dwóch sieci permutacji o $2^{k-1}$ wejściach. Wejścia i wyjścia łączymy następująco:

- $(2i-1)$-te wejście przekierowujemy do $i$-tego wejścia pierwszego układu przerzucającego, a później z $i$-tego wyjścia tego układu do $(2i-1)$-tego wyjścia
- $(2i)$-te wejście przekierowujemy do $i$-tego wejścia pierwszego układu przerzucającego, a później z $i$-tego wyjścia tego układu do $(2i)$-tego wyjścia
- Przed pierwszym układem permutującym dodajemy przerzutniki dla sąsiednich elementów.
	- Symetryczne przełączniki dodajemy po wyjściach

### Dowód Poprawności Poprzez Konstrukcję

Bierzemy dowolną permutację $\pi$ i wyznaczymy dla niej jakie przerzutniki mają *przerzucać*, by w ten sposób zmienić kolejność elementów. W tym celu przejdziemy przez graf (bo tak zgadliśmy albo przeczytaliśmy w mądrym paper).

Jeżeli chcemy uzyskać permutację $\pi$, to zdefiniujmy dla niej graf $G_{\pi}(V,E)$, gdzie:

- Zbiór $V = V_{I} \cup V_{O} \cup V_{M}$ składa się z:
	- $V_{I}$ wierzchołki odpowiadające portom wejściowym; $i$-temu wejściu odpowiada wejście $i$.
	- $V_{O}$ wierzchołki odpowiadające przełącznikom z ostatniej warstwy; $j$-ty przełącznik będzie oznaczany przez $i'',k''$ takie, że $\pi(i) = 2j-1\land \pi(k) = 2j$, czyli do tego przełącznika mają trafić dane z $i$-tego i $k$-tego wejścia.
	- $V_{M}$ pomocnicze wierzchołki etykietowane wartościami $1',2',\dots,n'$.
- Zbiór $E = E_{I} \cup E_{O} \cup E_{M}$ składa się z:
	- $\frac{n}{2}$ krawędzi łączących wierzchołki $(2i-1)\leadsto (2i)$.
	- $\frac{n}{2}$ krawędzi łączących wierzchołki $i'',k''$ odpowiadające $j$-temu przełącznikowi
	- $2n$ krawędzi przechodzących przez wierzchołki z $V_{M}$: $i\leadsto i'$ oraz $i'\leadsto i''$

**Lemat 2:**
Graf $G_{\pi}$ jest sumą rozłącznych cykli parzystych,
**d-d:**
Stopień każdego wierzchołka to $2$ oraz $G_{\pi}$ jest spójny. Dalej zauważamy, że *najmniejsze* każdy cykl składać może się jedynie z po $i$ wierzchołków z $V_{I},V_{O}$ oraz $2i$ wierzchołków z $V_{M}$.

Z [[Kolorowanie Grafu#Fakty|faktów o kolorowaniu Grafów]] i *lematu 2* wiemy, że $G_{\pi}$ ma dwukolorowanie. Teraz popatrzmy jakie własności spełnia to dwukolorowanie:

- Wierzchołki sąsiednich wejść mają różne kolory
- Wierzchołki o etykietach $i$ oraz $i''$ otrzymują ten sam kolor

Stąd wnioskujemy istnienie ustawienia przełączników realizującego $\pi$:

- Przełączniki z pierwszej warstwy ustawiamy tak, by wejścia pokolorowane na biało trafiły do *górnej* sieci permutującej.
- Przełączniki w górnej sieci permutacji ustawiamy tak, by permutowały zgodnie z $\pi$. Dokładniej, by *na wyjściu* były ustawione w takiej kolejności jak w $\pi$. To jest możliwe, bo *tak* (bo indukcja)
- Niech $i''$ będzie etykietą białego wierzchołka z $j$-tego przełącznika w ostatniej warstwie, a $k''$ etykietą czarnego wierzchołka. Jeśli $i$ poprzedza $k$ w permutacji $\pi$, to przełączamy na wprost, w przeciwnym razie zamieniamy.

![[Konstrukcja-sieci-przelaczajacej.jpg]]

### Koszt Konstrukcji

#### Głębokość Sieci

$$
\begin{align*}
G(n) &= \begin{cases}
G\left( \frac{n}{2} \right) + 2 &: n > 4 \\
2 &: \text{w p.p.}
\end{cases} \\
&= O(n)
\end{align*}
$$

#### Liczba Przełączników

$$
\begin{align*}
L(n) &= \begin{cases}
2L\left( \frac{n}{2} \right) + n &: n > 4 \\
4 &: \text{w p.p.}
\end{cases} \\
&= O(n \log n)
\end{align*}
$$
