## Własności

- Struktura:
	- Jest drzewem binarnym o wysokości $h$.
	- Wszystkie wierzchołki są na poziomie $h$ lub $h-1$.
	- Wszystkie liście na poziomie $h$ leżą *najbardziej na lewo*
		- To implikuje istnienie co najwyżej jednego wierzchołka z jednym synem
- Uporządkowanie:
	- Dla każdego wierzchołka $v$ będziemy chcieli, by $\text{val}(v) \ge \text{val}(\text{parent}(v))$.

> Budujemy kopiec dla minimów, ale dla maksimów jest *izomorficznie*.

## Reprezentacja Tablicowa

Okaże się, że kopiec można wygodnie trzymać w standardowej tablicy.
Jeżeli korzeń umieścimy pod indeksem $1$, to dla wierzchołka $v$ o indeksie $i_{v}$:

- Ojcem jest wierzchołek $\left\lfloor  \frac{i_{v}}{2}  \right\rfloor$
- Lewym synem jest $2i_{v}$
- Prawym synem jest $2i_{v} + 1$

## Operacja Zamiany Elementu

### Przesuwanie w Górę

Jeśli zmienimy element na mniejszy, to być może trzeba będzie go przesunąć w górę zamieniając jego miejsce z rodzicem.
Powtórzymy operację jeśli potrzeba dopóki ojciec nie będzie mniejszy.

### Przesuwanie w Dół

Jeśli zamienimy element na większy, to należy sprawdzić czy któryś z synów elementów nie jest mniejszy. Jeśli któryś jest, to należy wybrać mniejszy i zamienić go z aktualnym.
Krok należy powtarzać dopóki któryś syn jest mniejszy.

**Obserwacja:** przesuwanie w dół jest dwa razy droższe niż przesuwanie w górę (trzeba sprawdzić dwa elementy w każdym kroku).

## Operacje [[Kolejka Priorytetowa|Kolejkowe]]

### Insert

1. Dodaj element jako nowy liść w drzewie
2. Wykonaj [[#Przesuwanie w Górę]]

### Delete Min

1. Zamień miejscami `min` i *ostatni liść*
2. Zmniejsz rozmiar drzewa
3. Wykonaj [[#Przesuwanie w Dół]] dla korzenia

## Konstruowanie Kopca

### Od Góry

- Dla każdego elementu – $n$ razy
	- Dodaj element na koniec kopca – $O(1)$
	- Wykonaj operację [[#Przesuwanie w Górę|przesunięcia w górę]] – $O(\log n)$ (1)

(1) Nieformalnie zauważymy, że ostatni poziom drzewa binarnego składa się z $\frac{n}{2}$ elementów, oraz dla każdego z nich koszt *przesunięcia w górę* to $\log n$ bo idziemy przez całe drzewo.
Trochę bardziej formalnie robimy sumę:
$$
\begin{align*}
\sum\limits_{i=1}^{n}\lfloor \log_{2} i \rfloor &\approx \sum\limits_{i=1}^{\lfloor \log_{2} n \rfloor } 2^{i} \cdot i \\
&=2 - (\lfloor \log_{2}n  \rfloor + 1)2^{\lfloor \log_{2}n  \rfloor + 1} + \lfloor \log_{2}n  \rfloor \cdot 2^{\lfloor \log_{2}n  \rfloor + 2} \\
&= 2 - (2 \lfloor \log_{2}n  \rfloor - 1)2^{\lfloor \log_{2}n  \rfloor} = \Theta(n\log n)
\end{align*}
$$
Sumę liczymy wyznaczamy [[Sumowanie#Pochodna|pochodną]].

### Od Dołu

Będziemy konstruować kopce *od dołu*.
Zaczniemy od wszystkich liści. Są one poprawnymi kopcami o wielkości `1`.
Dalej będziemy chcieli połączyć sąsiednie kopce i dodać do nich korzeń. Będzie to wymagało co najwyżej przesunięcia w dół korzenia.

Intuicyjnie będzie *lepiej* dlatego, że praca potrzebna na dodanie wierzchołka będzie rosła z wysokością – dużo pracy zrobimy dla małej liczby wierzchołków (czyli inaczej niż poprzednio!).

By było trochę formalniej sumujemy łączną potrzebną pracę:
$$
\begin{align*}
\sum\limits_{i=1}^{n} \lfloor \log (n - i + 1) \rfloor &\approx \sum\limits_{i=1}^{\lfloor \log_{2}n \rfloor } \frac{2^{\lfloor \log_{2} n \rfloor}}{2^{i}} \cdot i \\
&\le 2^{\lfloor \log_{2} n \rfloor} \cdot \sum\limits_{i=1}^{\infty}\left( \frac{1}{2} \right)^{i} \cdot i \\
&= 2^{\lfloor \log_{2} n \rfloor} \cdot \frac{\frac{1}{2}}{\left( \frac{1}{2} \right)^{2}} \\
&= 4 \cdot 2^{\lfloor \log_{2} n \rfloor} = O(n)
\end{align*}
$$
Mamy trywialne ograniczenie $\Omega(n)$ ze względu na liczbę elementów stąd procedura działa w czasie $\Theta(n)$.