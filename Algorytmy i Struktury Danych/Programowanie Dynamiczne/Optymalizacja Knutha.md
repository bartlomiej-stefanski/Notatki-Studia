> Poza programem przedmiotu, ale *fajne*.

Liczenie dosyć standardowej tablicy programowania dynamicznego:
$$
dp[i][j] = \min_{k\in\{i, \dots, j\}} (dp[i][k-1] + dp[k+1][j])+ f(i, j) 
$$
Zajmuje zazwyczaj czas $O(n^{3})$.

Optymalizacja *Knutha* pozwala obniżyć ten czas do $O(n^{2})$ jeżeli zachodzą pewne warunki:

### Nierówność Czworoboku

Funkcja $f$ musi dla każdych $a\le b\le c\le d$ spełniać:
$$
f(a, c) + f(b, d) \le f(a, d) + f(b, c)
$$

### Monotoniczność Decyzji

Niech dla przedziału $dp[i][j]$ najlepsze wartości daje podział na $k_{ij}$.
Wtedy jeżeli zdefiniujemy następujące wartości:
$$
optk[i][j] = \text{argmin}_{k\in\{i, \dots, j\}}(p[i][k-1] + dp[k+1][j])
$$
gdzie $\text{argmin}_{k}(f(k))$ przyjmuje wartość $k$ dla którego $f(k)$ jest minimalne.

Dla tych wartości musi zachodzić
$$
optk[i][j-1] \le optk[i][j] \le optk[i+1][j]
$$
Intuicyjnie chcemy by rozszerzanie przedziału w prawo oraz skracanie z lewej strony zwiększało wartości $k$.

## Optymalizacja

Jeżeli zachodzą poprzednie własności, to zamiast przeszukiwać wszystkie $k$ wystarczy te wartości zawarte w przedziale:
$$
[optk[i][j-1], optk[i+1][j]]
$$
Gdyby tak nie było to możemy dojść do sprzeczności z którymś z warunków.
(tak, to koniec dowodu ~~tak naprawdę to coś więcej fajnie powiedzieć, ale...~~)

## Złożoność Czasowa

#TODO (dowód jakiś)