**Dane:**
Ciąg elementów $T[1\dots n]$ z porządkiem liniowym.

> Zakładamy bez straty ogólności, że liczby są różne.

**Zadanie:**
Znaleźć $k$-tą liczbę w kolejności według danego porządku.

Skorzystamy tutaj klasycznie z metody dziel i zwyciężaj. W każdym kroku będziemy dzielić wszystkie elementy na dwa rozłączne zbiory $U,V$ takie, że każdy element ze zbioru $U$ jest mniejszy od dowolnego elementu ze zbioru $V$.
Wtedy bazując na liczności zbioru $U$ dalsze poszukiwania wykonamy w zbiorze $V$ bądź $U$.

> Tak, trochę to przypomina [[Quicksort]], gdzie schodzimy tylko do jednego syna w drzewie rekursji.

Stąd oczywiście potrafimy napisać następujący pseudokod:
```
def selection(A[1..n], k):
	i = pseudomod(A)
	p = partition(A, i) // Operacja znana z quicksort
	if p >= k:
		return selection(A[1..p], k)
	else:
		return selection(A[p+1..n], k - p)
```

Pozostaje jedynie porządna implementacja funkcji `partition` tak, by za każdym razem dzielić przedziały prawie na pół.

### Partition

#### Magiczne Piątki 

Skorzystamy tutaj z [[Algorytm Magicznych Piątek]], który w liniowym czasie i stałej pamięci potrafi wyznaczyć element większy i mniejszy od co najmniej $\frac{3}{10}n - 4$ innych elementów.

Sprawi to, że na drzewo rekurencji będzie mieć logarytmiczną wysokość, a na każdym poziomie wykonamy liniową pracę -> algorytm działa ze złożonością $O(n)$.

### Algorytm Hoare'a

`partition` jest funkcją losującą element, wszystko bardzo podobnie do losowego quicksort.
Jak się [[AISD Lista 6#Zadanie 3|okazuje]] nadal działa w liniowym oczekiwanym czasie.
