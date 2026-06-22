## Counting Sort

**Dane:**
Ciąg liczb $A[1\dots n]$ całkowitych z przedziału $\langle l, r\rangle$.

**Rozwiązanie:**
Utworzymy tablicę na $k = r - l +1$ elementów i zapamiętamy ile jest elementów każdego rodzaju.

W ten sposób posortujemy liczby w czasie $O(n + k)$.

## Bucket Sort

**Dane:**
Ciąg liczb rzeczywistych $A[1\dots n]$ wylosowanych z przedziału $\langle l, r \rangle$ z jednorodnym rozkładem prawdopodobieństwa.

**Rozwiązanie:**
Podzielić liczby na $n$ rozłącznych przedziałów (kubełków), następnie posortować dowolnie (nawet kwadratowo).
Dalej mamy złożoność $O\left( n + n \cdot  S\right) = O(n)$, gdzie $S$ jest kosztem posortowania jednego kubełka.

Oczekujemy, że do każdego kubełka trafi $\Theta\left( \frac{1}{n} \cdot n \right)$ elementów, więc posortujemy je w czasie stałym.