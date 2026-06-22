# Szeregowanie Dla Pojedynczego Procesora

Dane jest $t_{1},t_{2},\dots,t_{n}\in\mathbb{N}$ będące czasami wykonania odpowiednio i-tego zadania dla $t_{i}$.

**Cel:** pokazanie porządku minimalizującego czas oczekiwania na ukończenie zadań:
$$\sum\limits_{i=1}^{n}(\text{czas na wykonanie i-tego zadania})$$

## Rozwiązanie

Chcemy wykonywać zadania od najkrótszego do najdłuższego.
Intuicyjnie zadania wykonane na początku zostaną policzone więcej razy.

Można pokazać, że dla każdego uszeregowania zadań, które nie jest posortowane rosnąco istnieje lepszy porządek.

### Gdzie [[Wstęp – Algorytmy Zachłanne|Zachłanność]]?

Wybierając następne zdanie do zrobienia bierzemy najtańsze które zostało do zrobienia.

## Dowód Poprawności

Niech permutacja $\pi = (i_{1},i_{2},\dots,i_{n})$ liczb wyznacza porządek rosnący kosztów zadań $t_{j}$.
Wtedy koszt możemy wyznaczyć następującą sumą:
$$
T(\pi) = \sum\limits_{k = 1}^{n} (n - k + 1)t_{i_{k}}
$$
Teraz załóżmy nie wprost, że istnieje *lepsza* permutacja $\pi'$, gdzie elementy $x,y$ ($x < y$) są zamienione miejscami, wtedy dla tej permutacji:
$$
\begin{align*}
T(\pi') = (n - x &+ 1)t_{i_{y}} + (n - y + 1)t_{i_{x}} + \sum\limits_{k = 1,k\ne x,y}^{n} (n - k + 1)t_{i_{k}} \\
T(\pi) - T(\pi') &= (n - x + 1)(t_{i_{x}} - t_{i_{y}}) + (n - y + 1)(t_{i_{y}} - t_{i_{x}}) \\
&= (y - x)(t_{i_{x}} - t_{i_{y}}) < 0
\end{align*}
$$
Ostatnia forma jest mniejsza niż zero, ponieważ $y > x \land t_{i_{x}} < t_{i_{y}}$.
Otrzymujemy więc sprzeczność, bo $\pi'$ ma większy koszt.

> Coś pewnie trzeba by było powiedzieć, że jeżeli żadna zamiana osobno nie polepsza wyniku, to jakieś ich złożenie również lepsze nie będzie.

# Szeregowanie z Terminami

**Dane:**

- Ciąg liczb naturalnych $d_{1},\dots ,d_{n}$ wyznaczających terminy wykonania zadań.
- Ciąg liczb rzeczywistych $g_{1},\dots,g_{n}$ wyznaczających zysk za wykonane zadanie.

> Każde zadanie wymaga jednej jednostki czasu.

**Zadanie:**
Wyznaczyć *wykonalny* podzbiór zadań $S\subseteq \{1,\dots,n\}$ maksymalizujący sumę $\sum\limits_{i\in S}g_{i}$.

***def:*** ciąg zadań $\langle i_{1}, i_{2}, \dots, i_{n}\rangle$ jest wykonalny jeżeli $\forall_{k\in\{1,\dots,n\}}k < d_{i_{k}}$. Zbiór zadań jest wykonalny jeżeli istnieje dla niego ciąg wykonalny.

## Strategia Zachłanna

Do zbioru zadań do wykonania dopisujemy zadanie o największym $g_{i}$ którego jeszcze nie wybraliśmy do wykonania pod warunkiem, że zdanie pozostanie wykonalne.

## Dowód Poprawności

Przypuśćmy , że nasz algorytm wyznacza zbiór zadań do wykonania $I$ różny od optymalnego $J$. Dla obu zbiorów definiujemy wykonywalne ciągi $\pi_{I},\pi_{J}$.
Na podstawie tych wykonywalnych ciągów utworzymy $\pi_{I}',\pi_{J}'$ gdzie wspólne zadania zaplanowane są na ten sam czas.
Następnie pokażemy, że zadania różne mają tą samą wartość.

### Przestawianie Zadań

Niech zadanie $a$ jest na różnych pozycjach $i,j$ w ciągach $\pi_{I},\pi_{J}$. Bez straty ogólności załóżmy, że chcemy to zadanie wykonać wcześniej w $\pi_{I}$ (czyli $i < j$).
W takim przypadku zamiana zadań na pozycjach $i,j$ w ciągu $\pi_{I}$ nie *zepsuje* ciągu zadań, ponieważ zadanie $a$ przesuniemy nie dalej niż jest w $\pi_{J}$ (a tam jest wykonalne) oraz drugie zadanie wykonamy wcześniej (czyli też na pewno nie zepsujemy).

### Równość Zysków

Weźmy dowolną pozycję $k$ na której ciągi $\pi_{I},\pi_{J}$ różnią się.

#### Oba Posiadają *Jakieś* Zadanie

- Jeżeli w $\pi_{j}$ brakowało by zadania, to moglibyśmy wziąć to z $\pi_{I}$ i otrzymać ciąg lepszy niż optymalny – sprzeczność.
- Jeżeli w $\pi_{I}$ brakowało by zadania, to mamy sprzeczność z działaniem algorytmu, który (ostatecznie) wybiera każde zadanie, które będzie mógł wykonać

#### Zadania Mają Ten Sam Zysk

Oznaczmy zadania na tej pozycji przez $i,j$. 

- Jeżeli $g_{i} < g_{j}$, to algorytm zachłanny rozpatrywał by wcześniej zadanie $j$ niż $i$, a jako że jest wykonywalne to by je wybrał – sprzeczność z działaniem algorytmu.
- Jeżeli $g_{i} > g_{j}$, to jakbyśmy wzięli zadanie $i$ zamiast $j$ w algorytmie optymalnym, to mielibyśmy większy zysk – sprzeczność z optymalnością.

Wnioskujemy więc, że na pozycjach na których znajdują się różne zadania ich zysk jest identyczny.

## Implementacja

**Lemat 1:**
Niech $J$ będzie zbiorem $k$ zadań i niech $\sigma = (s_{1},s_{2},\dots,s_{k})$ będzie permutacją tych zadań taką, że $d_{s_{1}} \le d_{s_{2}} \le \dots \le d_{s_{k}}$. Wtedy $J$ jest wykonalny $\iff$ $\sigma$ jest wykonalna.
**d-d:**
Dosyć intuicyjnie zadania, które trzeba zrobić wcześnie robimy maksymalnie wcześnie... (to nie jest formalne oczywiście).

### Naiwnie

Sortujemy zadania po kosztach $g$ malejąco oraz dla każdego liniowo sprawdzamy, czy można wstawić, jeżeli tak to przesuwamy elementy w tablicy i wstawiamy.
Daje to czas kwadratowy.

### [[Union Find]]

**Lemat 2:**
Zbiór zadań $J$ jest wykonalny $\iff$ następująca procedura ustawia wszystkie zadania z $J$ w ciąg wykonalny: dla każdego zadania, wykonaj je najpóźniej jak się da.
**d-d:**
Chyba widać?

**Obserwacja:**
Zadania będą się grupować w *ciągi zadań*.

Właśnie takie ciągi będziemy przechowywać w strukturze union-find. Dla każdego ciągu pamiętamy:

- `begin` – od jakiej pozycji się zaczyna
- `end` – na jakiej pozycji się kończy
- `taken` – czy pozycja jest zajęta
- `sum` – sumę zysków z zawartych elementów

Wtedy problem rozwiązujemy następująco:

- Dla każdego elementu `i` w kolejności malejących `g[i]`
	1. Wykonaj `pos = find(d[i])`
	2. Jeżeli nie jest zajęty, to zajmij, wpisz sumę itp.
	3. Jeżeli jest zajęty, to
		1. sprawdź, czy aktualny *ciąg zadań* można podłączyć do następnego (jeżeli nie ma wolnych miejsc)
		2. Ustaw `d[i] = pos.begin - 1` i wróć do punktu pierwszego
- Zlicz sumę ze wszystkich elementów w strukturze union-find

#### Złożoność Obliczeniowa

Jeżeli nie musimy sortować, to wystarczy nam złożoność union-find: $O(n\log^{*} n)$. W przeciwnym wypadku mamy $O(n\log n)$ z sortowania.

> To pewnie trzeba jakoś bardziej uzasadnić, ale tak będzie.