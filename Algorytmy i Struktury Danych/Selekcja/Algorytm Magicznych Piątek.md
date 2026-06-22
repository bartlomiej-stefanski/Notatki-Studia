**Dane:**
ciąg elementów $T[1,\dots, n]$ z porządkiem liniowym.

**Zadanie:**
Wyznaczyć przybliżenie mediany

## Algorytm

1. Podziel $T$ na fragmenty 5-elementowe (jeżeli w ostatnim jest miej to trudno.)
2. Ustal medianę każdego z tych zbiorów – zamień ją z pierwszym elementem fragmentu
3. Jeżeli jest tylko jeden fragment to wróć z medianą fragmentu
4. Utwórz *nowe indeksy* tak, by wskazywały na pierwsze elementy fragmentów
5. Wróć do punktu `1`

**Twierdzenie:**
Wyznaczona wartość jest nie mniejsza/większa niż $\frac{3}{10}n -4$ elementy.
**d-d:**
Po pierwszym podziale istnieje dokładnie $\left\lceil  \frac{1}{2} \left\lceil  \frac{n}{5}  \right\rceil  \right\rceil$przedziałów z medianą mniejszą/większą. W każdym z tych przedziałów istnieją co najmniej $3$ elementy większe/mniejsze.
Stąd już otrzymujemy $3\left\lceil  \frac{1}{2} \left\lceil  \frac{n}{5}  \right\rceil  \right\rceil \ge \frac{3n}{10} - 4$.

### Złożoność Obliczeniowa

Czas działania możemy oszacować od góry poprzez:
$$
T(n) = T\left( \left\lceil  \frac{n}{5}  \right\rceil  \right) + \Theta(n) = \Theta(n)
$$
> Dowodzimy z [[Dziel i Zwyciężaj#Złożoność Obliczeniowa Algorytmów Rekurencyjnych|twierdzenia o złożonościach]].


