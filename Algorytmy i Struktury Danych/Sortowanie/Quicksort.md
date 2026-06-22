Klasyczny algorytm sortujący oparty na strategii [[Dziel i Zwyciężaj]].
Algorytm składa się z dwóch głównych części:

- Wybór pivot – elementu wokół którego obracamy wszystkie inne
- Partition – obrót elementów wokół pivot

Podczas gdy optymalna implementacja partition jest dosyć oczywista (co nie oznacza, że *zupełnie* oczywista) to wybór pivot może zdecydować, czy nasza implementacja będzie działać w czasie kwadratowym, czy $n\log n$.

Sama procedura *quicksort* jest bardzo prosta:
```
fn quicksort(A[1..n]):
	if n < \eps:
		insert_sort(A)
		return

	p = choose_pivot(A)
	q = partition(A)
	quicksort(A[1..q])
	quicksort(A[q+1..n])
```

## Partition

Procedura partition dla tablicy `A[1..n]` przestawia elementy w taki sposób, by w pierwszej połowie znalazły się tylko takie mniejsze niż `A[p]`, a w drugiej tylko większe.

```
# Funkcja przyjmuje pozycję pivot jako argument p
fn partition(A[1..n], p):
	x = A[p]
	l = 1
	r = n
	while l < r:
		while A[l] <= x:
			l++
		while A[r] >= x
			r--
		
		if l < r:
			swap(A[i], A[j])
		else:
			break
	
	return A[j]
```

Intuicyjnie idziemy od obu stron wskaźnikami dopóki nie napotkamy elementu zbyt dużego/zbyt małego. Wtedy jeżeli *przeszliśmy zbyt daleko*, to kończymy, a jeśli nie, to zamieniamy wartości miejscami.

> Koszt tej procedury wynosi $\Theta(n)$.

## Wybór Pivot

Jest to najważniejszy punkt działania algorytmu. Słaby wybór pivot (np. taki, gdzie dzielimy $n$ elementowa tablicę na części jedno elementowe i $n-1$ elementowe) prowadzi do algorytmu o kwadratowej złożoności obliczeniowej.

Oczywiste jest również, że najlepszym wyborem była by mediana wszystkich elementów – wtedy w każdej iteracji dzielilibyśmy wszystkie elementy na dwie części co pozwalało by na uzyskanie złożoności $O(n\log n)$ ze wzoru $T(n) = T\left( \left\lfloor  \frac{n}{2}  \right\rfloor \right) + T\left( \left\lceil  \frac{n}{2}  \right\rceil \right) +\Theta(n)$.

Niezależnie od tego czy próbujemy wyznaczyć medianę, czy nie każdy model wybierania pivot można rozdzielić na dwie kategorie: deterministyczny i niedeterministyczny.

### Jeden element

Deterministycznie możemy wybierać np. pierwszy element tablicy, a nie deterministycznie można brać *losowy* element tablicy.
Oba warianty narażone są na *kwadracenie się*.
Dla deterministycznej wersji istnieje oczywisty przykład, dla losowej już nie, ale taka sytuacja zdarzy się tak samo często (więc trochę gorzej, bo nie wiemy kiedy będzie źle).

### Aproksymacja Mediany

Najprostszym sposobem jest wybranie mediany z trzech elementów.
Nie będzie to idealne, ale prawdopodobieństwo złego wyboru spada znacząco.

Praktycznie można to implementować poprzez losowanie trzech elementów lub deterministyczne wybranie pewnych trzech (dobrym pomysłem może być pierwszy, ostatni i środkowy).

### Dokładna Mediana?

Jest to możliwe do wyznaczenia w czasie liniowym, więc pozwoliło by zachować złożoność $O(n\log n)$, ale okaże się, że stałe występujące w algorytmie będą na tyle duże, że okaże się to niepraktyczne do zastosowań w prawdziwym świecie (zwłaszcza, że istnieją dosyć dobre estymatory mediany).

## Oszacowanie Oczekiwanego Kosztu Działania

### Wprost

Pokażmy, że jeżeli jako pivot wybierany jest losowy element tablicy, to oczekiwana złożoność obliczeniowa wynosić będzie $\Theta(n\log n)$.

Niech dana będzie tablica do podziału o $n$ elementach: $A[1..n]$:
$$
\text{rank}(x, A[1..n])\overset{def}{=} |\{j : 1 \le j \le n \land A[j] \le x\}|
$$
> Intuicyjnie od ilu elementów tablicy $A$ argument $x$ jest nie mniejszy.

W momencie wywołania procedury partition dla $x = A[p]$ mamy losowy element, więc:
$$
P(\text{rank}(x, A[1..n]) = i) = \frac{1}{n}
$$
Co jest bardzo spodziewane, bo w końcu mamy n elementów które można wybrać jako podział...

Wynik procedury `partition` (który element jest pivot'em) zależy oczywiście od wartości wyrażenia $\text{rank}$. Gdy $\text{rank}$ dla $A[p]$ równa jest $i$, to funkcja `partition` zwróci  $i - 1$.
Otrzymujemy więc wartość $0$ z prawdopodobieństwem $\frac{2}{n}$ (dla $rank$ równego $1$ i $n$), a wszystkie inne z [[Przestrzeń Probabilistyczna#Prawdopodobieństwo|prawdopodobieństwem]] $\frac{1}{n}$.
Stąd czas działania wyraża się następującym wzorem:
$$
\begin{align*}
T(n) = \begin{cases}
1 &: n =1  \\
\frac{1}{n}\left( T(1) + T(n-1) + \sum\limits_{d=1}^{n-1}(T(d) + T(n-d)) \right) + \Theta(n) &:\text{w p.p}
\end{cases}
\end{align*}
$$
Teraz liczymy wszystko po kolei...
$$
\frac{1}{n}(T(1) + T(n-1)) = O(n)
$$
Oznacza to, że możemy pominąć ten składnik, ponieważ jest on już uwzględniony w $\Theta(n)$.

Czas teraz rozpisać pozostałą część sumy. Na początek zauważymy, że każdy składnik sumy uwzględniamy dwukrotnie, więc całość można przepisać jako:
$$
T(n) = \frac{2}{n}\sum\limits_{d = 1}^{n-1}T(d) + \Theta(n)
$$
Teraz *wyczarujemy*, że złożoność obliczeniowa której szukamy to $n\log n$, więc wystarczy sprawdzić, czy dobrze wyczarowaliśmy:
$$
\begin{align*}
T(n) = \frac{2}{n}\sum\limits_{d=1}^{n-1}T(k) + \Theta(n) \le an\log n + b
\end{align*}
$$
Naszym zadaniem jest pokazać, że odpowiednie stałe $a, b$ istnieją. Weźmy $b$ wystarczająco duże by $T(1) \le b$, wtedy:
$$
\begin{align*}
T(n) = \frac{2}{n}\sum\limits_{k = 1}^{n-1}(ak\log k + b) + \Theta(n) \le \frac{2a}{n}\sum\limits_{k=1}^{n-1}k\log k + \frac{2b}{n}(n-1) + \Theta(n)
\end{align*}
$$
Dalej należy udowodnić oszacowanie $\sum\limits_{k=1}^{n-1}k\log k \le \frac{1}{2}n^{2}\log n - \frac{1}{8}n^{2}$.
To pozwoli na dalsze szacowanie nierówności:
$$
\begin{align*}
\sum\limits_{k=1}^{n-1}k\log k &\le ((\log n) - 1) \sum\limits_{k=1}^{\lceil n/2 \rceil -1}k + \log n\sum\limits_{k=\lceil n/2 \rceil }^{n-1}k \\
&=\log n\sum\limits_{k=1}^{n-1}k - \sum\limits_{k=1}^{\lceil n/2 \rceil -1}k  \\
&\le \frac{1}{2}n(n-1)\log n - \frac{1}{2}\left( \frac{n}{2} - 1\right) \frac{n}{2} \\
&\le \frac{1}{2}n^{2} \log n - \frac{1}{8}n^{2}
\end{align*}
$$
A z tego można już napisać, że:
$$
\begin{align*}
\frac{2a}{n}\left( \frac{1}{2}n^{2} \log n - \frac{1}{8} n^{2} \right) + \frac{2b}{n}(n-1) + \Theta(n) &\le an\log n - \frac{a}{4}n + 2b + \Theta(n) \\
&= an\log n + b + \left( \Theta(n) + b - \frac{a}{4}n \right) 
\end{align*}
$$
Ostatnią składową można pominąć dobierając $a$ trak, by $\frac{a}{4}n \ge \Theta(n) + b$.
To kończy dowód,  że $T(n) \le an\log n + b$ dla pewnych stałych $a,b$.

### Wersja Która Nie Boli...

Zdefiniujmy *specjalną wersję* algorytmu quicksort (czasem nazywaną *insistent quicksort*) taką, która wywołuje się rekurencyjnie jedynie dla podziałów, które gwarantują podział równiejszy niż $1:3$. Jeżeli wylosujemy nie dobry podział, to powtarzamy wybieranie pivot.

Takie działanie gwarantuje, że głębokość drzewa rekurencji nie przekracza [[Symbole Asymptotyczne|asymptotycznie]] $\log n$.

Na każdym wierzchołku drzewa rekurencji wykonamy również liniowo wiele pracy (szansa na dobry podział wynosi $\frac{1}{2}$, więc oczekujemy jednego nadmiarowego wybrania pivot co jedynie zmieni stałą przy współczynniku liniowym).

Dalej dowolnym sposobem można sumować wartości w wierzchołkach drzewa, a otrzymamy złożoność $n\log n$.

> Ten dowód można również przenieść na dowód złożoności *zwykłego* quicksort, jeżeli pokażemy, że złe podziały nie są gorsze niż ponowne losowanie.

## Usprawnienia Quicksort

Jest to *najszybszy* algorytm sortowania oparty na porównaniach, ale by był *jeszcze szybszy* możemy wprowadzić do niego kilka modyfikacji.

### Trójpodział

Jeżeli podejrzewamy, że wartości, które zamierzamy sortować będą często się powtarzać to dobrym pomysłem może być zastosowanie funkcji `partition`, która zwróci dwa przedziały do sortowania nie uwzględniające elementów o wartości pivot.

### Eliminacja Rekursji

#### Nie-rekurencyjne Sortowanie Małych Pod-przedziałów

Jeżeli do posortowania zostało nam niewiele elementów, to skorzystamy jakiegoś prostego algorytmu o małych stałych (nawet kwadratowego).

#### Implementacja Nie-rekurencyjna

Trochę boli, ale ten algorytm można zaimplementować nie używając rekurencji.
Wtedy zaoszczędzimy liniowo-wiele pamięci potrzebnej normalnie na stos wywołań.