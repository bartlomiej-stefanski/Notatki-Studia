**Dane:**
Rodzina zbiorów $S = \{S_{1},S_{2},\dots,S_{k}\}$ podzbiorów $n$-elementowego uniwersum $U$.
Funkcja kosztów $c:S\to \mathbb{R}_{+}$.

**Zadanie:**
Znaleźć najtańszą podrodzinę $S$ pokrywającą $U$; formalnie szukamy $S' \subseteq S$ takiej, że $\cup_{X\in S'}X = U$ oraz wartość funkcji $\text{koszt}(Z) = \sum\limits_{X\in Z}c(X)$ jest minimalna.

Dla tego problemu możemy wymyślić wiele strategii zachłannych, które wydaje się, że mogły by działać, np.:

- Wybierz podzbiór pokrywający najwięcej elementów
- Wybierz najtańszy podzbiór
- Wybierz podzbiór, który najtaniej pokrywa elementy
- ...

Dla każdej z tych strategii istnieje jednak kontrprzykład.
Problem ten okazuje się być NP trudny stąd nie powinno nas to dziwić.

## Algorytm Aproksymacyjny

Skoro nie potrafimy znaleźć rozwiązania optymalnego, to może chociaż uda się znaleźć takie, które będzie rozsądnie blisko?

Zdefiniujmy funkcję $\text{cne} : S \times U \to \mathbb{R}$:
$$
\text{cne}(S_{i}, C) = \frac{c(S_{i})}{|S_{i} \setminus C|}
$$
> Intuicyjnie wyznaczamy średni koszt za dodanie nowego elementu.

### Strategia

Zaczynając od $C = \emptyset$ będziemy wybierać kolejne $S_{i}$ o najmniejszej wartości $cne$ aż do pokrycia całego zbioru $U$.

#### Oszacowanie Od Góry
**Twierdzenie:**
Ta strategia znajduje rozwiązania nie gorsze asymptotycznie niż od logarytm od $OPT$.
**d-d:**
Niech $e_{1},e_{2},\dots,e_{n}$ będzie ciągiem elementów uniwersum wypisanych w kolejności pokrywania ich przez algorytm. Jeśli pokrywanym elementom przypiszemy cenę równą wartości $cne$ podzbioru, który je pokrywa, to koszt pokrycia możemy wyrazić jako sumę cen elementów:
$$
cena(e_{i}) < \frac{OPT}{n - i + 1}
$$
Jest tak dlatego, że:

- Pokrywając $i$-ty element zostało nam co najmniej $n-i+1$ innych do pokrycia
- Elementy te można by pokryć zbiorami z rozwiązania optymalnego, więc to będzie nasze ograniczenie od góry (jak algorytm weźmie lepsze to *fajnie*, ale nie na to patrzymy tutaj)

Całkowity koszt szacujemy teraz od góry jako:
$$
\sum\limits_{i=1}^{n}cena(e_{i}) < \sum\limits_{i=1}^{n} \frac{OPT}{n - i + 1} = H_{n}OPT \approx \ln n \cdot OPT
$$

#### Oszacowanie Od Dołu

Oszacować od dołu można przez przykład: [[AISD Lista 2#Zadanie 9]].