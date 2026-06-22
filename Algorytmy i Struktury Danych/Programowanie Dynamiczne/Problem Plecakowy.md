**Dane:**

- $w_{1},w_{2},\dots,w_{n}$ – wagi przedmiotów
- $v_{1},v_{2},\dots,v_{n}$ – wartości przedmiotów
- $W\in\mathbb{N}$ – pojemność plecaka

**Zadanie:**
wybrać przedmioty o łącznej wadze mniejszej niż $W$ w taki sposób, by suma ich wartości była maksymalna.
Dodatkowo mamy wariant z powróżeniami przedmiotów i bez powtórzeń.

> Większość problemów plecakowych w tym te omawiane tutaj są NP-trudne.

## Wariant z Powtórzeniami

Zauważmy, że naturalnie potrafimy definiować pod-problemy dla problemu plecakowego.
Niech $dp[w] = \text{maksymalna wartość plecaka o pojemności } w$. Wtedy najlepsze możliwe zapakowanie plecaka o pojemności $W$ odpowiada $\max_{i}\{dp[W - w_{i}]+v_{i}\}$ co prowadzi nas do mniejszego problemu. Z tej obserwacji otrzymujemy następujące równanie:
$$
dp[i] = \begin{cases}
0 &: i \le 0 \\
max_{i}\{k(W - w_{i} ) + v_{i}\} &: \text{w p.p.}
\end{cases}
$$
Na wykonanie tego algorytmu potrzebujemy czasu $O(nW)$.

> Algorytm jest pseudo-wielomianowy – czas działania zależy również od danych, nie tylko ich rozmiaru.

## Wariant Bez Powtórzeń

Tym razem zauważamy, że redukcję do pod problemów możemy wykonać poprzez ograniczenie zbioru możliwych przedmiotów. Zdefiniujemy więc: 
$$
dp[w][j] = \text{maksymalna wartość plecaka o pojemności }w\text{ z przedmiotami } 1,\dots ,j
$$
To również prowadzi nas do równania rekurencyjnego:
$$
\begin{align*}
dp[w][j] = \begin{cases}
0 &: w = 0 \lor j= 0 \\
\max\{dp[w-w_{j}][j-1] + v_{j}, dp[w][j-1]\} &: \text{w p.p.}
\end{cases}
\end{align*}
$$
> Intuicyjnie dla każdej pozycji *bierzemy* $j$-ty element lub nie.

Ten algorytm również działa w czasie $O(nW)$.