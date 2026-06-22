> Czasem w literaturze nazywane "drzepcem".

Struktura ta jest [[Binary Search Tree|binarnym drzewem wyszukiwań]] opartym na obserwacji, że jeżeli do drzewa BST będziemy dodawać elementy w losowej kolejności, to oczekiwana wysokość jest $O(\log n)$.
Oczywiście do takiej konstrukcji musimy mieć dostęp do wszystkich elementów *na początku*, co nie zawsze będzie możliwe.

Rozwiązaniem jest obserwacja, że *losową kolejność* można interpretować jako kolejne *wagi kopcowe*. Wtedy po konstrukcji drzewo spełnia zarówno niezmienniki BST jak i kopca.
Jeżeli dodamy do drzewa nowy wierzchołek, to losujemy dla niego wagę i *zmieniamy strukturę drzewa* tak, by spełniało wszystkie niezmienniki kopca i BST.

**Twierdzenie 1:**
Istnieje dokładnie jeden drzewiec dla danych kluczy i wag (bez straty ogólności zakładamy, że są różne).
**d-d:**
Jedno-elementowe drzewo można utworzyć na jeden sposób.
Zakładamy indukcyjnie, że każde $k < n$ elementowe drzewo można utworzyć na dokładnie jeden sposób.
Dalej obserwujemy, że dane jednoznacznie wyznaczają nam korzeń (wierzchołek z najmniejszą wagą).
Ten wierzchołek z kolei wyznacza jednoznacznie zbiory mniejsze niż $n$ z których będziemy budować lewe i prawe poddrzewo. Z indukcji zbudujemy je na jeden sposób.
Korzeń i poddrzewa mamy jednoznacznie zdefiniowane, więc całe drzewo również.

> Widzimy więc, że wstawienie nowego wierzchołka z losową wagą jest identyczne do budowania kopca od podstaw już z tym wierzchołkiem

---

**Twierdzenie 2:**
Drzewiec ma oczekiwaną wysokość rzędu $O(\log n)$.
**d-d:**
Dowód przebiega podobnie do dowodu [[Quicksort#Wersja Która Nie Boli...|quicksort]] – pokazujemy, że prawdopodobieństwo podziału lepszego niż $1:3$ wynosi $0.5$. Wnioskujemy z tego, że każda gałąź drzewa składa się z wierzchołków na których występuje *dobry* podział (tych wierzchołków jest $\log n$ wiele) oraz pewnej ilości wierzchołków ze słabym podziałem.
Dalej wyznaczamy wartość oczekiwaną długości ciągu *słabych* podziałów, wyjdzie nam $2$. Oczekujemy więc, że nie rzadziej niż co trzy poziomy dokonamy *dobrego* podziału – wysokość pozostaje więc ograniczona przez logarytm.

## Operacje

Drzewiec pozwala wykonywać standardowe operacje słownikowe, wykonywać będziemy je tak jak dla standardowego drzewa BST, główną różnicą będą rotacje które będziemy wykonywać dodatkowo w celu naprawy u porządku kopcowego.

> Rotacje nie psują porządku BST, ale pozwalają dowolnie zmienić strukturę drzewa. Wnioskujemy więc, że będą one wystarczające (kluczowe jest jednak *ile* rotacji wystarczy).

##### Insert

Wstawiamy element jak *standardowo w BST*, by następnie dla wstawionego elementu wykonywać rotacje odwracające relacje jego i rodzica dopóki element jest mniejszy niż rodzic.

##### Delete

Usuwamy *standardowo* tak jak w BST. Jeżeli usuwaliśmy coś innego niż liść, to potrzebujemy wykonać rotacje, by przesunąć element w dół

#### Ograniczenie Na Rotacje

Pesymistycznie ograniczamy liczbę rotacji przez wysokość drzewa – być może trzeba przenieść nowy wierzchołek do korzenia.
Pesymistyczne ograniczenie na wysokość to $O(n)$, ale z bardzo dużym prawdopodobieństwem będzie ona rzędu $O(\log n)$.

Można jednak *lepiej*. Przeprowadzimy analizę na liczbę rotacji potrzebną do usunięcia elementu (później pokażemy, że uogólnia się ona na dodawanie).

##### Analiza Rotacji Przy Usuwaniu

Niech $G_{m}$ wyznacza elementy na *prawym kręgosłupie* lewego syna $m$. Łatwo zauważyć, że przesuwając wierzchołek na pozycję liścia będziemy musieli wykonać co najmniej $|G_{m}|$ rotacji, bo każda usunie co najwyżej jeden element z tego kręgosłupa.

Dalej zdefiniujmy zmienną losową $X_{i,k}$:
$$
X_{y,x} = \begin{cases}
1 : y \text{ jest na prawym kręgosłupie lewego poddrzewa } x\\
0 : \text{w p.p.}
\end{cases}
$$
Teraz pokażemy, że $X_{y,x} = 1$ zachodzi tylko wtedy, gdy:

1. $x$ ma mniejszą wagę kopcową niż $y$ – oczywiste
2. klucz $y$ jest mniejszy niż $x$ – oczywiste
3. Dla każdego $z$, takiego, że $key(y) < key(z) < key(x)$ waga kopcowa $y$ jest mniejsza niż $z$
	- $(\Rightarrow)$ Wtedy większe elementy niż $z$ są w prawym poddrzewie $y$
	- $(\Leftarrow)$ Skoro nie ma wierzchołka którego $y$ (lub jego przodkowie) byli by lewym synem, to $y$ jest na prawym kręgosłupie

> Zmienną losową rozpatrujemy tylko dla elementów lewego poddrzewa.

Obliczymy teraz prawdopodobieństwo $X_{y,x}$ – z warunków wypisanych powyżej wnioskujemy, że spośród wag kopcowych elmentów z kluczami zawartymi w przedziale $[key(y), key(x)]$, waga $x$ musi być najmniejsza, a waga $y$ druga najmniejsza – tylko wtedy nie będzie istniało w tym przedziale $z$, które popsuło by warunek $(3)$.
Liczymy więc liczbę możliwych permutacji wag w których zachodzi taka kolejność:
$$
P(X_{y,x} = 1) = \frac{(key(x) - key(y) - 1)!}{(key(x) - key(y) + 1)!} = \frac{1}{(key(x) - key(y) + 1)(key(x) - key(y))}
$$
> Zakładamy, że klucze są ze zbioru $\{1, \dots, n\}$, żeby działało i nie definiować jakiś funkcji w stylu *ile elementów zawiera się pomiędzy...*

To pozwoli nam policzyć wartość oczekiwaną prawego kręgosłupa lewego poddrzewa $E(L)$ jako sumę wartości oczekiwanej wszystkich $X_{y,k}$. Oczywiście dla elementów nie spełniających dwóch pierwszych warunków przyjmie ona zero. Dla pozostałych będziemy mieć:
$$
\begin{align*}
E(L_{x}) &= \sum\limits_{i, key(i) < key(x)}E(X_{i,x}) \\
&= \sum\limits_{i, key(i) < key(x)} P(X_{i,x} = 1) \\
&= \sum\limits_{i, key(i) < key(x)} \frac{1}{(key(x) - key(i) + 1)(key(x) - key(i))} \\
&\overset{(1)}{=} \sum\limits_{i=1}^{key(x)-1} \frac{1}{(key(x) - i + 1)(key(x) -i)} \\
&= \sum\limits_{i=1}^{key(x)-1} \frac{1}{i(i+1)} = 1 - \frac{1}{key(x)}
\end{align*}
$$
> $(1)$ przenosimy się z kluczy na liczby naturalne, bo wybraliśmy zbiór kluczy jako $\{1,\dots,n\}$, więc klucze mniejsze niż $key(x)$ to liczby $\{1,\dots,key(x) -1\}$.

Symetrycznie wnioskujemy dla lewego kręgosłupa prawego drzewa, co w końcu da nam oczekiwaną liczbę rotacji jako:
$$
E(L_{x}) + E(R_{x}) = 2 - \epsilon
$$

#### Operacje Słownikowe

Tak jak dal *zwykłych* BST możemy zdefiniować operacje na zbiorach (`union`, `split`).