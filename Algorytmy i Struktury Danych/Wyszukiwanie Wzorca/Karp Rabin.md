Dla wzorca $P$ wyliczamy funkcję [[Haszowanie|haszującą]], podobnie dla fragmentu $T[1..m]$ tekstu. Tylko jeżeli hasze są równe faktycznie porównujemy elementy wzorca i tekstu.

Kluczowa będzie możliwość wyznaczenia hasz fragmentu $T[i+1..i+m]$ na podstawie $h(T[i..i+m-1])$.
Jeżeli $h(T[i..i+m-1]) = \sum\limits_{j=0}^{m-1}d^{m-j}\cdot T[j+i]$, to następny hasz otrzymamy następująco:
$$
\begin{align*}
h(T[i+1..i+m]) = h(T[i..i+m-1]) \cdot d - T[i]\cdot d^{m} + d\cdot T[i+m]
\end{align*}
$$
Wszystko można wziąć brać po modulo, by nie dochodziło do przepełnienia.

## Złożoność Czasowa

Pesymistycznie taka jak algorytmu naiwnego – by wystąpił taki przypadek kolizje haszy muszą wystąpić na (prawie) każdej pozycji.  
Tak może być jeżeli faktycznie wzorzec występuje na każdej pozycji tekstu. Mamy więc ograniczenie $O(mn)$.

Częściej będziemy spodziewać się jednak czasu działania $O(n + m)$.