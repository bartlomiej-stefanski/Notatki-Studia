**Dane:**
Ukorzenione drzewa $T_{1},T_{2}$.
Założymy, że składają się z tej samej liczby wierzchołków i mają tą samą wysokość (inaczej zadanie jest trywialne).

**Zadanie:**
Stwierdzić, czy drzewa są izomorficzne.

## Kluczowy Pomysł

Wędrując przez wszystkie poziomy będziemy sprawdzać, czy w obu drzewach istnieje tyle samo izomorficznych poddrzew zaczynające się w wierzchołkach aktualnego poziomu.

### Algorytm

Dla każdego wierzchołka będziemy chcieli wyznaczyć funkcję $\text{kod(v)}\rightarrow\mathbb{N}$ (realizowaną praktycznie jako pole struct).
Zaczynając od najniższego poziomu $h$, przechodzimy po wszystkich i dla $i$-tego wykonujemy:

1. Wyznacz $S_{i}$ – zbiór wierzchołków $i$-tego poziomu niebędących liściem
2. Dla każdego wierzchołka $v\in S_{i}$ wyznacz wektor kluczy $K_{i}[v]$ zawierający posortowane wartości $\text{kod}$ wszystkich synów $v$
3. Posortuj [[Sortowanie Leksykograficzne|leksykograficznie]] $K_{i}$
4. Jeżeli $K_{1}\ne K_{2}$, to zakończ nie znajdując izomorfizmu
5. Dla każdego wierzchołka $v\in S_{i}$ ustal $\text{kod(v)}$ na wartość *ile różnych kluczy było do tej pory*
6. Ustal kod liści aktualnego poziomu na $-1$

> Można przeprowadzić łatwy dowód poprzez indukcję na drzewach po ich wysokości.

### Złożoność Czasowa

Zauważmy, że każdy wierzchołek obu drzew przetwarzamy stałą ilość razy:

- Sprawdzamy czy jest liściem
- Przypisujemy $\text{kod}$
- Podpinamy jako syn innego elementu
- Uczestniczymy w sortowaniu leksykograficznym – raz przetwarza każdy wierzchołek
- Porównujemy *klucze* ojców

Czas działania jest więc liniowy względem ilości wierzchołków w obu drzewach.
