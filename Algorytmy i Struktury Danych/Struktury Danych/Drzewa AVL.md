> Nazwa AVL pochodzi od nazwisk twórców algorytmu: *Adelsona-Velskiego i Landisa*.

Jest to [[Zbalansowane Drzewa|zbalansowane]] [[Binary Search Tree|drzewo przeszukiwań binarnych]],  w którym **wysokość lewego i prawego poddrzewa różni się o co najwyżej jeden.**
Jest to główna cecha tych drzew pozwalająca osiągać im asymptotyczny czas $O(\log n)$ dla wstawiania i usuwania elementów.

**Fakt:**
W dowolnym drzewie binarnym wierzchołków jest o jeden mniej niż *brakujących liści*.

**Twierdzenie:**
Wysokość drzewa AVL wynosi co najwyżej $1.4405\log(n + 2)$.
**d-d:**
Niech $p(h) =$ *liczba brakujących liści w minimalnym drzewie AVL o wysokości* $h$.
Pokażmy indukcyjnie, że $p(i) = F(i + 2)$, gdzie $F(n)$ oznacza $n$-tą [[Liczby Fibonacciego|liczbę Fibonacciego]].

- $p(1) = 2,\ p(2) = 3$ – można sprawdzić wszystkie możliwości.

Teraz indukcyjnie zakładamy tezę dla $k < n$ i pokazujemy tezę dla $n$:

Wiemy, że korzeń będzie mieć dwójkę dzieci. Jeżeli ma mieć minimalnie wiele wierzchołków, to prawe poddrzewo będzie o wysokości $n-1$, a lewe $n-2$. Oba będą składać się z minimalnie wielu wierzchołków. Korzeń ma obu synów, więc otrzymujemy:
$$
p(n) = p(n-1) + p(n-2) = F(n+2)
$$
Teraz z własności liczb Fibonacciego mamy, że dla $n$ wierzchołkowego drzewa jego wysokość $h$:
$$
n + 1 > \frac{1}{\sqrt{ 5 }}\left( \frac{1 + \sqrt{ 5 }}{2} \right)^{h + 2} -1
$$
Dalej zostają tylko przekształcenia algebraiczne.

## Operacje na Drzewie

### Wstawianie

Początkową część wykonujemy tak jak w standardowych algorytmach dla [[Binary Search Tree]]. Ciekawie robi się dopiero jak wracamy do korzenia.

Wracając musimy w każdym odwiedzonym wierzchołku sprawdzić, czy nie zepsuliśmy balansu. Jeżeli zepsuliśmy, to trzeba naprawić! Jeżeli bez straty ogólności założymy, że zepsuliśmy lewe poddrzewo, to mamy dwa istotnie różne przypadki do rozpatrzenia.

![[AVL-tree-insert.png|400]]

Zauważamy, że w obu przypadkach wysokość drzewa (mierzona od korzenia, którym być może jest inny wierzchołek!) nie została zmieniona.
Wnioskujemy z tego, że wystarczą co najwyżej dwie rotacje krótkie lub bardziej abstrakcyjnie *jedno naprawienie balansu*.

### Usuwanie

Niestety znacznie bardziej skomplikowane...
Zaczynamy od znalezienia wierzchołka $v$ do usunięcia i sprawdzenia z czym pracujemy. Jeżeli $v$ jest liściem, lub posiada jednego syna, to sytuacja samego usuwania jest trywialna.
Jeżeli $v$ jest gdzieś *w środku* drzewa, to zamieniamy $v$ z bezpośrednim następnikiem/poprzednikiem w porządku elementów (który jest trywialnie usuwalny) i od razu usuwamy $v$ z nowej pozycji.

Gorsza część zaczyna się, gdy trzeba posprzątać niezmiennik dotyczący wysokości drzewa. Okazuje się bowiem, że tym razem rotacje mogą być wymagane w niemal wszystkich wierzchołkach drzewa.
Jest tak dlatego, że rotacje mogą nie zachować wysokości, przez co problem kaskadowo idzie w górę.

### Złożoność Czasowa

Wstawianie i usuwanie wymaga przeprowadzenia wyszukiwania na drzewie [[Binary Search Tree|BST]] o wysokości $O(\log n)$ i wykonania stałej liczby operacji dla każdego wierzchołka na drodze (nawet jeśli tą operacją jest rotacja).
