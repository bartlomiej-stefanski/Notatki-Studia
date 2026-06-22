Algorytm znajdujący [[Drzewo Spinające#Minimalne Drzewo Spinające|Minimalne Drzewo Spinające]] dla grafu $G(V,E)$.

## Strategia

Niech $E'$ wyznacza zbiór wybranych krawędzi (początkowo pusty). Zbiór krawędzi $E$ ustaw w kolejności rosnących wag krawędzi, następnie przeglądnij je.

Dla każdej krawędzi, jeżeli dodanie jej do $E'$ nie utworzy cyklu w grafie $G(V, E')$, to dodaj tą krawędź.

## Dowód Poprawności

Na koniec algorytmu Dodane zostaną wszystkie krawędzie, które nie tworzą cyklu -> będzie ich $n-1$ dla grafu spójnego -> zwracane jest drzewo spinające.

Pokażmy, że wartość zwrócona przez algorytm – $S$ równa jest $T$  – pewnemu MST składającego się z maksymalnie wielu początkowych krawędzi $S$. Załóżmy nie wprost, że $S$ i $T$ są różne.
Oznaczmy krawędzie w tych MST: $E(S) = (e_{1},e_{2},\dots)$, $E(T) = (p_{1},p_{2},\dots)$.
Skoro $S$ i $T$ są różne, to istnieje najmniejsze takie $i$, że $e_{i}\ne p_{i}$.

Bez krawędzi $e_{i}$ drzewo $S$ zostanie podzielone na dwie spójne składowe $X,Y$.
Krawędź $e_{i}$ jest najmniejszą łączącą $X,Y$, bo jeżeli istniała by mniejsza, to przejrzelibyśmy ją wcześniej algorytmem Kruskala i wzięli do $S$, a wtedy jeżeli $X,Y$ były by spójne i mielibyśmy nadal krawędź $e_{i}$, to istniał by cykl.

Zauważmy, że $E \cup \{e_{i}\}$ zawiera cykl, bo w $T$ musi istnieć jakaś krawędź łącząca $X,Y$ – teraz istnieją dwie.
Wiemy, że $e_{i}$ jest najtańszą taką krawędzią, więc *tą inną* krawędź tworzącą cykl można zamienić na $e_{i}$ by otrzymać tańsze MST. Sprzeczność z optymalnością $T$.