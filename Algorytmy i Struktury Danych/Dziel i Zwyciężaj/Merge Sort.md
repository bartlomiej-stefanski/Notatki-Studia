> *Kanoniczny* problem dla [[Dziel i Zwyciężaj]].

**Dane:**

- Wartości $v_{1},v_{2},\dots,v_{n}$.
- Operacja $<$ dla tych wartości.

**Zadanie:**

Wyznaczyć permutację $\pi = (p_{1},\dots ,p_{n})$ zbioru $\{1,2,\dots ,n\}$ taką, że:
$$
\forall_{i} v_{p_{i}} < v_{p_{i+1}}
$$

> Po co ja to piszę, przecież każdy wie o co chodzi w sortowaniu...

## Strategia

Zauważamy, że:

- Łatwiej sortuje się krótsze sekwencje
- Łatwo podzielić sekwencję na dwie krótsze (np. na pół)
- Łatwo połączyć dwie posortowane sekwencje

Na podstawie tej strategii możemy rozpisać następujący algorytm:
```
def merge_sort(A[1..n]):
	if n == 1:
		return A
	
	merge_sort(A[1..n/2])
	merge_sort(A[(n+1)/2..n])
	
	# l, r to nowe tablice
	l, r = A[1..n/2], A[(n+1)/2..n]

	inx = 1
	linx = 1
	rinx = 1
	while linx <= l.size && rinx <= r.size:
		if l[linx] < r[rinx]:
			A[inx++] = l[linx++]
		else:
			A[inx++] = r[rinx++]
	
	while linx <= l.size:
		A[inx++] = l[linx++]
	while rinx < r.size:
		A[inx++] = r[rinx++]
```

Czemu dzielimy na dwie części, a nie na więcej, skoro dwie przyspieszyły?
Okaże się, że większa liczba tablic do złączenia znacząco utrudnia to działanie.

## Złożoność Obliczeniowa

Do rozwiązania mamy prostą zależność rekurencyjną:
$$
T(n) = 2T\left( \frac{n}{2} \right) + \Theta(n) = \Theta(n\log n)
$$
> Wyciągamy to z [[Dziel i Zwyciężaj#Złożoność Obliczeniowa Algorytmów Rekurencyjnych|wzoru na złożoność]].