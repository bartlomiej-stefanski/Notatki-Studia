Niektórych problemów nie można rozwiązać używając jedynie porównań.
Np. dla poniższego zbioru punktów niemożliwe jest wyznaczenie otoczki wypukłej wykonując jedynie porównania pomiędzy punktami:
![[Otoczka-wypukla-punkty.svg]]
Każde porównanie $A,B,C$ z $D,E$ przyjmuje tą samą wartość, a jednak oczekiwane odpowiedzi są oczywiście różne.

Dla takich problemów niezbędne są drzewa decyzyjne *wyższego rzędu*.

---

Liniowe drzewa decyzyjne pozwalają przyrównywać [[Kombinacja Liniowa|kombinację liniową]] elementów do zera:
$$
\sum\limits_{i}\alpha_{i}x_{i} \overset{?}{=} 0
$$
Gdzie:

- $x_{i}$ kolejny element danych interpretowany jako liczba rzeczywista
- $\alpha_{i}$ współczynnik przy danych

### Interpretacja

Dane dla problemów dla liniowych drzew decyzyjnych będziemy interpretować jako $n$-elementowe wektory $\langle x_{1},x_{2},\dots,x_{n} \rangle$ wskazujące punkt $(x_{1},x_{2},\dots,x_{n})$ należący do przestrzeni $\mathbb{R}^{n}$.
Wtedy każde przyrównanie kombinacji liniowej do zera odpowiada podzieleniu przestrzeni hiperpłaszczyzną.

**Lemat:**
Obszary przestrzeni wyznaczane przez hiperpłaszczyzny są wypukłe.
**d-d:**
Można indukcyjnie, wtedy:

- Przestrzeń jest wypukła
- Podział wypukłej przestrzeni hiperpłaszczyzną jest wypukły

> Nie formalnie i na szybko, ale prawdopodobnie jest to *znany fakt*.

#### Znowu Drzewa?

By potrafić szacować złożoność algorytmów na podstawie głębokości liści w drzewach musimy na początku zdefiniować drzewa...
W przypadku *liniowych* drzew decyzyjnych:

- Korzeń *odpowiada* całej przestrzeni.
- Każdy wierzchołek nie będący liściem trzech synów oraz definiuje kombinację liniową.
	- Lewy syn *odpowiada* przestrzeni na lewo od płaszczyzny
	- Prawy syn *odpowiada* przestrzeni na prawo od płaszczyzny
	- Środkowy syn *odpowiadający* płaszczyźnie

Dla tego modelu mogą więc przebiegać znane ze *zwykłych* drzew analizy polegające na zliczaniu liści, bo stała liczba synów nie wpływa na asymptotyczną złożoność.

**Fakt:**
Przestrzenie odpowiadające liściom są podziałem przestrzeni.

## Przykład

### Różność Elementów

**Dane:**
$x_{1},x_{2},\dots,x_{n}\in\mathbb{R}$

**Zadanie:**
Czy istnieje $i\ne j$ takie, że $x_{i} = x_{j}$.
Oczekiwana jest odpowiedź `TAK` lub `NIE`.

##### Analiza

Popatrzmy na ciągi $x_{1},\dots,x_{n}$ jak na punkty z $\mathbb{R}^{n}$.
Weźmy dowolne dwie (różne) permutacje zbioru $\{1,\dots ,n\}:$ $P_{i},P_{j}$. Niech $k$ będzie najmniejszą liczbą, która występuje na różnych pozycjach w obu permutacjach, odpowiednio $k_{i}, k_{j}$.

**Fakt:**
Każde $P_{i},P_{j}$ zawarte będzie w liściu z odpowiedzią `TAK`.

**Lemat 1:**
Permutacje $P_{i},P_{j}$ należą do innych liści (obszarów przestrzeni).
**d-d:**
Weźmy punkty odpowiadające permutacjom: $P_{i} = (i_{1},\dots,i_{n}), P_{j} = (j_{1},\dots,j_{n})$. Wtedy dla tych punktów zachodzi możemy zdefiniować funkcję $d((x_{1},\dots,x_{n})) = x_{k_{i}} - x_{k_{j}}$.
Teraz bez utraty ogólności załóżmy, że $i_{k_{i}} < i_{k_{j}}$, a wtedy:
$$
\begin{align*}
d(P_{i})  < 0 && d(p_{j}) > 0
\end{align*}
$$

> Wybraliśmy najmniejszy element o różnych pozycjach w permutacjach, więc $j_{k_{i}} < j_{k_{j}}$ prowadziło by do sprzeczności,  bo mamy różne elementy, najmniejszy różny był na pozycji $k_{i}$ w $P_{i}$, więc *jeszcze mniejszy* nie może być na pozycji $k_{i}$ w $P_{j}$, bo wzięlibyśmy go jako mniejszego.

Teraz jeżeli narysujemy prostą pomiędzy punktami $P_{i},P_{j}$, to *z liniowości* funkcji $d$ wnioskujemy, że przyjmuje gdzieś wartość $0$ – wtedy elementy $x_{k_{i}},x_{k_{j}}$ są równe.
Oznacza to, że prosta pomiędzy tymi punktami przecina hiperpłaszczyznę budującą granice obszaru, a dalej z wypukłości obszarów wnioskujemy, że $P_{i},P_{j}$ są w różnych liściach.

Permutacji jest $n!$, więc wymaganych jest co najmniej $n!$ liści.
Drzewo o takiej wysokości będzie mieć wysokość co najmniej $\Omega(n \log n)$.

### Otoczka Wypukła

[[AISD Lista 5#Zadanie 2|Lista 5, zadanie 2]].

### 3SUM

[[AISD Lista 5#Zadanie 3|Lista 5, zadanie 3]].
