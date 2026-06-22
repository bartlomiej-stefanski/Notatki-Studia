Algorytm znajdujący [[Drzewo Spinające#Minimalne Drzewo Spinające|Minimalne Drzewo Spinające]].

> Algorytm działa z założeniem, że wagi krawędzi drzewa są różne. Jeżeli nie są należy utworzyć na nich porządek.

## Działanie Algorytmu

Drzewo spinające powstaje poprzez wykonanie wielu iteracji algorytmu.

Niech na początek zbiór wybranych krawędzi $E'$ będzie pusty.
Dla każdego wierzchołka wybierzmy najtańszą krawędź wychodzącą i dodajmy ją do $E'$. Po jednej iteracji będziemy mieć co najwyżej $\frac{n}{2}$ silnie spójnych składowych.

Następnie potraktujmy powstałe silnie spójne składowe jak wierzchołki i utwórzmy z nich graf, gdzie pomiędzy dwoma SSS istnieje krawędź wtedy i tylko wtedy, gdy istnieją w nich wierzchołki połączone w oryginalnym grafie krawędzią.
Algorytm powtarzamy dla grafu SSS dopóki zawiera więcej niż jeden wierzchołek.

Na koniec zbiór $E'$ będzie zawierał wierzchołki MST.

> Zmniejszanie liczby składowych co najmniej dwukrotnie w każdej iteracji prowadzi do czasu działania $O(n\log(n))$ – takiego jak w innych algorytmach wyznaczających MST.

## Dowód Poprawności

### Krawędzie $E'$ Nie Tworzą Cyklu

Jeżeli cykl istnieje w pewnym *super-wierzchołku*, to powstał poprzez wcześniejsze połączenie przynajmniej dwóch super-wierzchołków. Rozważmy przypadki:

- Cykl powstał w wyniku połączenia dwóch super-wierzchołków -> użyto dwóch różnych krawędzi do połączenia dwóch wierzchołków, obie powinny być minimalne, sprzeczność.
- Cykl powstał w wyniku połączenia super-wierzchołków $v_{1},v_{2},\dots,v_{n}$ -> koszty krawędzi muszą być $c(\{v_{1},v_{2}\}) < c(\{v_{2},v_{2}\}) < \dots < c(\{v_{n},v_{1}\})$, więc otrzymujemy sprzeczność, bo nie wzięlibyśmy $\{v_{n},v_{1}\}$.

### Krawędzie Tworzą MST w Każdym Kroku

Załóżmy, że super-wierzchołek $V_{i}$ nie jest MST optymalnym dla swojego podzbioru wierzchołków. *Jakieś* MST istnieje, nazwijmy je $T$. Skoro są różne, to istnieje krawędź $e_{i}\in E(V_{i})\land e_{i}\notin E(T)$. Dodanie $e_{i}$ do $T$ będzie skutkować powstaniem cyklu. Istnieje więc inna krawędź wybrana jako wychodząca dla wierzchołków łączonych $e_{i}$. Algorytm Boruvki wybrał najmniejszą wychodzącą z obu, więc można zamienić $e_{i}$ na mniejszą krawędź i nadal otrzymać MST. Sprzeczność, bo $T$ miało być minimalne.

Załóżmy, że dla pewnej iteracji mamy zbiór poprawnych super-wierzchołków. Załóżmy nie wprost, że po tej iteracji otrzymamy nie-najmniejsze drzewo rozpinające wierzchołków $V_{i}$ (względem optymalnego $T$).
Dalej argument jak wewnątrz super-wierzchołka.