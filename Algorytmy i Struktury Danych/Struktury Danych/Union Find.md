Struktura danych pozwalająca na następujące operacje:

- `find(i)` – znalezienie identyfikatora podzbioru, do którego należy `i`.
- `union(p, q)` – połączenie podzbiorów, do których należy `p`, `q`.
	- Czasem `union` definiujemy dla identyfikatorów zbiorów, ale to prawie nic nie zmienia.

**Założenia:**

- Liczba elementów zbioru wszystkich elementów jest znacząco mniejsza niż pamięć wewnętrzna.
- Wykonanych zostanie $c \cdot n$ instrukcji `uinion`/`find`.

> Algorytm można rozwiązywać online lub offline; my robimy wersję online.

## Naiwne Rozwiązanie

Przechowujemy tablicę, która dla każdego elementu wyznacza *id* zbioru w którym się znajduje.

- `find(i)` – zwraca *id* z odpowiedniego indeksu tablicy
- `union(p, q)` – przegląda wszystkie elementy tablicy i tym w podzbiorze `p` ustala wartości *id* dla `q`

Oczywiście `find` działa w $O(1)$, a `union` w $\Theta(n)$.  
Jeżeli wykonamy wszystkie możliwe `union` otrzymamy czas kwadratowy co jest dosyć wolne.

## Listy

Organizujemy wszystkie podzbiory $U$ w listy. Dla operacji `union(a, b)` dołączamy krótszą listę do dłuższej zaznaczając wszystkie elementy krótszej jako przynależne do dłuższej (przechodzimy *liniowo* tylko po elementach krótszej listy).

Okazuje się, że już ta poprawa pozwoli wykonać $O(n)$ dowolnych operacji w czasie $O(n\log n)$.

> Dowód można oprzeć na obserwacji, że najbardziej kosztowne `union` występuje, gdy łączone zbiory są równoliczne. Stąd dzielimy cały czas na dwa i *powstaje* logarytm.

## Drzewa

Każdy podzbiór zbioru $U$ reprezentujemy jako drzewo z wyróżnionym korzeniem. Każdy wierzchołek odpowiadający elementowi z $U$ zawiera wskaźnik na ojca w drzewie (lub `Null` dla korzenia).  
Dla wygody potrzebna nam będzie tablica mapująca zewnętrzne elementy na wierzchołki o następującej strukturze:

```c
struct Vertex {
	Vertex* parent{ NULL };
	int subtree_count{1};
} elements[...];
```

### Implementacja

#### Union(a, b, c)

Wykonując instrukcję połączymy drzewa `a`, `b` w jedno, którego korzeń będzie wskazywać na etykietę `c`.  
Będziemy chcieli dołączyć mniejsze (licznościowo) drzewo do większego.

> Jeżeli chcemy obsługiwać union, które nie podają korzeni poddrzew, to wystarczą dodatkowe wywołania `find`, które nie pogorszą złożoności.

#### Find(i)

To polecenie wykonamy przechodząc od wierzchołka do korzenia (z którego potrafimy wyznaczyć etykietę).  
Dodatkowo każdy wierzchołek odwiedzony na drodze podłączymy od razu do korzenia.

### Złożoność Obliczeniowa

**Lemat 1:**  
Każde drzewo o wysokości $h$ ma nie mniej niż $2^h$ wierzchołków.  
**d-d:**  
Indukcyjnie, $T(n):$ drzewo o wysokości $n$ ma $2^n$ wierzchołków.

- $T(0)$ oczywiście spełnione, bo składa się z jednego wierzchołka
- $T(n)$ wysokość drzewa wzrośnie tylko, gdy łączyć będziemy dwa drzewa o tej samej wysokości. Dwa drzewa o wysokości $n-1$ mają łącznie $2\cdot2^{n-1} = 2^n$ wierzchołków.

Dalej niech  $\hat{\sigma}$ wyznacza ciąg operacji `union` z ciągu $\sigma$ po wyrzuceniu wszystkich `find`.

***def:*** $\text{rząd}$ wierzchołka $v$ względem $\hat{\sigma}$ jest wysokość $v$ w lesie powstałym po wykonaniu ciągu operacji $\hat\sigma$.

**Lemat 2:**  
Jeżeli w trakcie wykonania $\hat{\sigma}$ wierzchołek $u$ staje się potomkiem $v$, to przed doczepieniem $\text{rząd}(u) \le \text{rząd}(v)$, a po doczepieniu nierówność jest ostra.  
**d-d:**  
Wynika to bezpośrednio z tego w jaki sposób łączymy drzewa oraz niezmienności rzędu dla wierzchołków innych niż korzenie (ale wtedy co najwyżej zwiększamy 'większy' z rzędów korzeni, więc po doczepieniu nierówność jest ostra).  
**Wniosek:**  
Idąc od dowolnego wierzchołka w górę będziemy przechodzić do wierzchołków o mniejszej randze.

**Lemat 3:**  
W drzewie, którego korzeń $v$ ma rząd $r$ jest co najmniej $2^{r}$ wierzchołków.  
**d-d:**  
Skoro ma rząd $r$, to ma wysokość również jest $r$. Dalej z *(lematu 1)* otrzymujemy, że w takim drzewie będzie nie mniej niż $s^{r}$ wierzchołków.

**Lemat 4:**  
W drzewie jest co najwyżej $\frac{n}{2^{r}}$ wierzchołków o randze $r$.  
**d-d:**  
Z *lematu 3* każdy taki wierzchołek ma poddrzewo o wielkości $2^{r}$ oraz poddrzewa są różne, bo rzędy są ściśle rosnące na ścieżce do korzenia.

#### Funkcja Log*

***def*:**
$$
\begin{align*}
A(i) &= \begin{cases}
0 : i=0\\
2^{A(i-1)}
\end{cases}\\
\log^{*}n &= \min\{k : A(k) \ge n\}
\end{align*}
$$
Słownie $\log^{*} n$ wyznacza najmniejsze takie $k$, że funkcja Ackermana $A(k)$ jest nie mniejsza niż $n$.

> Funkcja $\log*$ rośnie bardzo wolno, w praktyce traktuje się ją jako stałą.
> Jest to funkcja *pseudo-odwrotna* do [[Funkcja Ackermana|funkcji Ackermana]].

---

Teraz podzielmy wszystkie wierzchołki na kubełki takie, że $B_{i} = \{v \mid \log^{*}(\text{rząd}(v)) = i\}$.

1. Wystarczy nam $\log^{*}n$ kubełków, bo nie może istnieć wierzchołek o randze większej niż $n$.
2. W kubełku $B_{i}$ jest co najwyżej $\frac{2n}{2^{A(i)}}$ elementów. Z *lematu 4* możemy rozpisać sumę na maksymalną liczbę elementów każdej z rang: $\frac{n}{2^{A(i)}} + \frac{n}{2^{A(i) + 1}} + \dots + \frac{n}{2^{2^{A(i)} - 1}} \le \frac{2n}{2^{A(i)}}$.

Dalej wydzielmy czasy działania trzech części działania operacji `find`:

- $T_{1} = \sum\limits_{\sigma}\text{(przejście do korzenia)}$
- $T_{2} = \sum\limits_{\sigma}\text{(przejścia pomiędzy kubełkami)}$
- $T_{3} = \sum\limits_{\sigma}\text{(przejścia wewnątrz kubełków)}$

Wtedy oczywiście łączny kosz wykonania wszystkich operacji `find` wynosi $T = T_{1} + T_{2} + T_{3}$.
Do korzenia przejdziemy raz dla każdego zapytania, stąd $T_{1} = O(n)$.  
Mamy ograniczenie na liczbę kubełków, stąd $T_{2} = O(n\log^{*}n)$ – każdym elementem przejdziemy co najwyżej każdy kubełek (tak, to jest luźne oszacowanie).

By oszacować $T_{3}$ przeanalizujmy przechodzenie z pewnego wierzchołka $u$ do $v$ – najwyższego wierzchołka w tym kubełku – $B_{i}$ (zakładamy, że $v$ nie jest korzeniem całego drzewa, bo wtedy przejście liczymy w $T_{1}$).  
Z wierzchołkiem $u$ będziemy iść w górę drzewa, więc w kolejnych operacjach przenosić będziemy się do ściśle mniejszej wartości $\text{rząd}$ (*lemat 2*).

Różnych wartości $rząd$ w jednym kubełku będzie nie więcej niż $2^{A(i)} - A(i) \le 2^{A(i)}$, stąd też nie wykonamy więcej przejść w jednym kubełku.  
Pozwoli to nam rozpisać odgórne oszacowanie $T_{3}$ jako suma wszystkich możliwych przejść *"do góry kubełka*:
$$
T_{3} \le \sum\limits_{i = 1}^{\log^{*}n}\sum\limits_{v \in B_{i}}2^{A(i)} \le \sum\limits_{i = 1}^{\log^{*}n} \frac{2n}{2^{A(i)}} 2^{A(i)} = 2n\log^{*}n
$$

> To oszacowanie jest *bardzo* nie precyzyjne, ale wystarcza na nasze potrzeby.

Dla każdego wierzchołka nie liczymy drogi *do samego korzenia*, bo będzie ona uwzględniona w elemencie sumy odpowiadającym pierwszemu elementowi z niższego kubełka do którego wejdziemy (samo przejście do niższego kubełka liczymy w $T_{2}$!).  
To wystarczy, bo każdą taką ścieżkę przejdziemy co najwyżej raz – każdy odwiedzony wierzchołek dołączymy do korzenia, więc dalej wystarczą elementy z sumy $T_{1}$.

---

Dostajemy więc na koniec oszacowanie:
$$
T = T_{1} + T_{2} + T_{3} = O(n\log^{*}n)
$$
