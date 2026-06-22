Ta struktura będzie modyfikacją pomysłu [[Kopce Dwumianowe|kopców dwumianowych]], która pozwoli na zaimplementowanie dodatkowej operacji `decrement(node, v)` zmniejszającej wartość elementu `node` o `v` działającą w amortyzowanym czasie stałym.

> W kopcach dwumianowych można taką operację zaimplementować w czasie $O(\log n)$ – wymaga to przesuwania elementu do góry.

## Struktura

Wyjdziemy od modelu znanego z kopców dwumianowych w wersji *lazy* – lasu drzew pamiętanego w cyklicznej liście oraz wskaźnika na minimum.
Zrelaksujemy jednak ścisłe wymagania dotyczące kształtu drzew.

Dodamy za to jedno pole logiczne do każdego wierzchołka drzewa, które będzie przechowywać informacje *"czy wierzchołek utracił jednego ze swoich synów w wyniku operacji `cut`"*.

> Nie nazywamy tego pola, ale *pamiętamy*, że istnieje.

## Operacje

Do analizy zamortyzowanej wykorzystamy niezmiennik z kopców dwumianowych oraz dodamy jeden nowy:

- Na każdym drzewie w liście odłożone są `2`  żetony
- Na każdym wierzchołku z odciętym jednym synem położone są `3` żetony

### Insert, findmin, meld

Wykonujemy tak jak dla [[Kopce Dwumianowe#Operacje Lazy|kopców dwumianowych w wariancie leniwym]].

### Cut

 Wywołanie operacji `cut(p)` odłącza `p` od swojego ojca (jeśli istnieje) i dołącza go do listy wszystkich elementów (operacja meld). Jeżeli ojciec `p`: `p'` utracił już jednego syna, to wykonujemy rekurencyjnie `cut(p')` aż do napotkania wierzchołka bez odciętego syna lub korzenia.

#### Analiza Zamortyzowana

Operacja kosztuje nas `6` żetonów:

- Jeden wykorzystujemy na *operacje niskiego poziomu*
- W zależności od tego który z kolei element ucinamy od rodzica:
	- Pierwszy -> kładziemy `2` żetony na nowym drzewie i `3` żetony na rodzicu
	- Drugi -> kładziemy `2` żetony na nowym drzewie, podnosimy `3` z rodzica, by mieć do dyspozycji łącznie `6` i wykonujemy `cut(p')`

### Decrement

Operacja `decrement(p, v)` zmniejsza o `v` wartość przechowywaną w `p`. Jeżeli psuje to porządek kopcowy, to wykonujemy dodatkowo `cut(p)`.

#### Analiza Zamortyzowana

Operacja kosztuje nas `7` żetonów.

- Jeden wykorzystujemy na operacje niskiego poziomu.
- Pozostałe zostaną użyte do wykonania `cut` jeżeli będzie potrzebny

### Deletemin

Wykonujemy tak jak dla kopców dwumianowych.

#### Analiza Zamortyzowana

Przebiega również jak dla kopców dwumianowych – nie zajmujemy się tutaj utrzymywaniem drugiego niezmiennika dotyczącego kredytów, a pierwszy jest taki sam.

To co trzeba za to pokazać, że wystarczy nam logarytmicznie wiele rzędów drzew.

**Lemat:**
Dla kopca Fibonacciego drzewo rzędu $i$ ma co najmniej $F_{i}$ elementów, gdzie $F_{i}$ oznacza $i$-tą liczbę [[Liczby Fibonacciego|Fibonacciego]].
**d-d:**
Zauważamy, że drzewa rzędu $0,1$ składają się z co najmniej $1$ elementu, co zgodne jest z liczbami Fibonacciego (definiujemy od $1,1$).
Dalej indukcyjnie zakładamy, że drzewo rzędu każde drzewo rzędu $i < k$ ma nie mniej niż $F_{i}$ elementów, z tego argumentujemy:
Drzewo $k$-tego poziomu składa się z drzew $0,1,\dots k-1$. W najgorszym przypadku, możemy odciąć drzewo $(k-1)$ poziomu i obcinać drzewa niższych poziomów tak, by były minimalnie małe. Wtedy ilość wierzchołków w drzewie $k$-tego poziomu wyrażana będzie sumą:
$$
1 + \sum\limits_{i=0}^{k-2}F_{i} = F_{k}
$$
> Znana własność liczb Fibonacciego

Liczby Fibonacciego rosną wykładniczo, więc faktycznie wystarczy nam logarytmicznie wiele rzędów na przechowanie $n$ elementów.

***UWAGA:***
Nie oznacza to, że wysokość kopców Fibonacciego ograniczona jest przez logarytm!!!!

### Delete?

Okazuje się, że za darmo możemy dodać operację `delete` usuwającą element.
Będzie ona składać się z wywołania $\text{decrement}(p, -\infty)$, a następnie `deletemin`.

Złożoność będzie więc logarytmiczna.

> W takiej samej złożoności można napisać tą funkcję dla kopców dwumianowych.

