> Algorytm Knutha-Morrisa-Pratta

[[Wyszukiwanie Automatem Skończonym]] wymaga, by dla każdego prefiksu wzorca istniała funkcja przejścia *dla każdej* następnie napotkanej litery. Wprowadza to duże koszty generowania automatu, bo takich możliwych przejść jest po prostu dużo (dokładnie to $m|\Sigma|$ wiele).

Głównym pomysłem stojącym za KMP jest zrelaksowanie tych wymogów, by dla każdego stanu przejście przy braku trafienia wyznaczało następne *potencjalne* miejsce do zaczęcia dalszych poszukiwań (a nie to, gdzie na pewno można).  
Będzie to oznaczało więcej obliczeń podczas wyszukiwania wzorca, ale na razie nas to nie interesuje.

## Funkcja $\pi$

Dla wzorca $P$ definiujemy *funkcję prefiksową* $\pi : \{1,\dots,m\} \to \{0,\dots,m-1\}$:
$$
\pi(q) = \max\{k \mid k < q \land P_{k} \text{ jest sufiksem } P_{q}\}
$$
> Intuicyjnie: jeżeli dopasowaliśmy prefiks o długości $q$, to funkcja $\pi$ wskazuje jaki najdłuższy (ale krótszy od $q$) prefiks wzorca dopasuje się do sufiksu przejrzanego fragmentu tekstu.

### Wyznaczanie Funkcji $\pi$

```
def find_pi(P[1..m]):
	pi[] = {0}  # inicjalizacja tablicy zerami
	k = 0
	for q in 2..m:
		while k > 0 && P[k + 1] != P[q]:
			k = pi[k]
		
		if P[k+1] == P[q]:
			k += 1
			pi[q] = k
	
	return pi
```
Dla każdej kolejnej litery wzorca 

> W każdym kroku *"trochę jakby"* dopasowujemy *krótsze* prefiksy wzorca do *aktualnego* prefiksu.

#### Przykład

Napis `aaabaca` będzie mieć następującą tablicę $\pi$:
```
# Indeksowane od 1
 1  2  3  4  5  6  7
[0, 1, 2, 0, 1, 0, 1]
 a  a  a  b  a  c  a
```

Czyli np.: `pi[5] = 1`, bo *najdłuższy krótszy* prefix `aaaba` będący sufiksem `aaaba` to `a`.

## Szukanie Dopasowań

Jeżeli dana jest funkcja $\pi$, to naturalny będzie algorytm, gdzie przechodzimy po kolei po elementach tekstu i próbujemy każdym przedłużyć aktualnie dopasowany prefiks. Jeżeli to się nie uda, to próbujemy ponownie z *najdłuższym, ale krótszym* prefiksem.

```
def kmp_match(T[1..n], P[1..m]):
	pi = find_pi(P)
	q = 0
	for i in 1..n:
		while q > 0 && P[q+1] != T[i]:
			q = pi[q]
		
		if P[q+1] == T[i]
			tne q += 1
		if q == m:
			# wzorzec występuje na przedziale T[i-m+1..i]
```

### Złożoność Czasowa

W `kmp_match` główna pętla `for` wykona się $\Theta(n)$ razy.  
Dla każdego z tych przejść środkowa pętla `while` wykona się co najwyżej $q\le m$ razy.   Zauważamy jednak, że zmienną `q` zwiększamy co najwyżej o jeden przy każdym przejściu `for`, więc koszt wewnętrznej pętli `while` amortyzuje się do $O(n)$.

Dla funkcji `find_pi` można przeprowadzić identyczne rozumowanie, tylko że długość ciągu wynosi $m$.

Łączny kosz działania algorytmu wynosi więc $O(n + m)$.