Kopce dwumianowe pozwalają na szybkie i łatwe wykonywanie standardowych operacji kopcowych (`insert`, `makeheap`, `findmin`, `deletemin`), a ponadto `meld` – łączenia kopców.

> Praktycznie operacja `meld` może posłużyć do implementacji `join_pqueue` dla kolejek priorytetowych.

***Def:***
Drzewo dwumianowe $B_{i}$ składa się z $i$ poddrzew: $B_{0},B_{1},\dots,B_{i-1}$:
![[binomial-tree-example.png]]

**Fakt:**
Drzewo $B_{i}$ zawiera $2^{i}$ wierzchołków.

***Def:***
Niech $T$ będzie drzewem. Rzędem wierzchołka w $T$ nazywamy liczbę jego dzieci. Rzędem drzewa $T$ jest rząd jego korzenia.

## Kopiec Dwumianowy

***Def:***
Kopiec dwumianowy to zbiór drzew dwumianowych, które pamiętają elementy z uporządkowanego uniwersum zgodnie z porządkiem kopcowym.

> By zapis implementacji był wygodny zakładamy, że dla każdego wierzchołka lista jego dzieci jest cykliczna.

### Łączenie Drzew Dwumianowych

Operację wykonywać będziemy jedynie dla drzew o tym samym rozmiarze.
Całość operacji polega na podłączeniu jednego drzewa do korzenia drugiego:
![[Binomial-heap-join.png|400]]
Koszt takiej operacji wynosi więc $O(1)$.

### Operacje Eager

Kopiec składa się z tablicy wskaźników na kopce kolejnych rozmiarów (`NULL`, gdy nie ma takiego kopca).
Dodatkowo przechowujemy wskaźnik na kopiec z najmniejszym elementem uaktualniany co insert/deletemin.

#### Insert

Tworzymy jedno elementowy kopiec.
Dalej w pętli zaczynając od $i=0$ dopóki istnieje w tablicy kopiec o wielkości $i$:

- Połącz *dodawany kopiec* i kopiec o wielkości $i$, by uzyskać kopiec o wielkości $i+1$
-  Wyczyść zapisany kopiec pod $i$
- Ustal aktualny kopiec jako rezultat `join`
- Ustal $i \leftarrow i+1$

Jak w końcu znajdziemy $i$ dla którego nie ma kopca w tabeli, to po prostu wpisujemy w to miejsce nowy kopiec.

##### Analiza Złożoności

Robimy analizę zamortyzowaną. Niech `insert` kosztuje nas `3` żetony, użyjemy ich w następujący sposób:

1. Zostawimy na stercie ostatecznego rozmiaru
2. Używamy do utworzenia początkowego jedno-elementowego drzewa
3. Używamy do uaktualnienia minimum

Żetony potrzebne do wykonywania kolejnych `join` będziemy podnosić z drzew, które chcemy łączyć.

Wnioskujemy więc, że koszt zamortyzowany koszt `insert` to $O(1)$.

#### Meld

Operacja łączenia dwóch kopców $h,h'$.
*Dodajemy* drzewa zawarte w $h'$ do tablicy kopcowej z $h$ przechodząc od najmniejszych do największych. To będzie trochę izomorficzne z dodawaniem binarnym – w każdym momencie będziemy mieli co najwyżej trzy kopce danego rozmiaru, więc w stałym czasie wybierzemy *jeden* odpowiedniego rozmiaru.

##### Analiza Złożoności

Zajmie to nam co najwyżej czas $\log n$, bo tyle co najwyżej jest różnych kopców.

#### Deletemin

Po usunięciu minimum otrzymujemy rodzinę drzew kopcowych $\{B_{0},\dots,B_{i}\}$. Tworzymy z nich kopiec (mamy to od razu), a następnie wykonujemy `meld` z oryginalną instancją kopca.

Dodatkowo przeglądamy wszystkie elementy w tablicy, by ustalić wskaźnik na minimum.

##### Analiza Złożoności

Taka jak `meld` + $O(\log n)$.

### Operacje Lazy

Tym razem będziemy chcieli, by jeszcze dodatkowo operacja `meld` była w czasie stałym – zrobimy to kosztem `deletemin`, które będzie logarytmiczne.

W tym celu zmieniamy wewnętrzną reprezentację kopca w taki sposób, by przechowywał on cykliczną listę zawartych w nim drzew. Wskaźnik na kopiec minimalny jak ostatnio.

Do analizy złożoności będziemy zachowywali niezmiennik: *na każdym drzewie dwumianowym w liście są odłożone $2$ żetony*.

#### Insert

Tworzy nowe drzewo jedno-elementowe, dodaje je do listy i uaktualnia wartość minimum.

Koszt tej operacji to $3$ kredyty – jednym płacimy za stałą liczbę operacji, a drugi odkładamy na nowo utworzone drzewo.

#### Meld

Dla danych dwóch kopców $h,h'$ łączymy ich listy oraz *minimalizujemy minimum*., by zwrócić nowy kopiec.

To kosztuje nas $1$ kredyt, którym płacimy za wykonywane operacje (których jest stała ilość).

#### Deletemin

Usuwamy wskazywane minimum w rezultacie czego otrzymujemy las drzew, które dołączamy do listy łączonej (`meld`).

Dalej wykonamy *czyszczenie* kopca – połączymy przechowywane elementy list tak, by uzyskać poprawny kopiec dwumianowy.

W tym celu możemy posłużyć się tablicą drzew jak w metodzie *eager*.
Dalej po kolei przejdziemy przez wszystkie elementy linked listy, by dodać je do tablicy, lub jeżeli pole jest już zajęte wykonać merge i zapisać do innego pola.

Na koniec należy naprawić wskaźnik na minimum (przeglądamy całą tablicę zanim zrobimy z niej listę)

##### Analiza Złożoności

Zauważmy, że łącznie i przeglądanie drzew możemy opłacić z żetonów przechowywanych na drzewach.
Będziemy zachowywali niezmiennik: *każdy element w tablicy ma na sobie jeden żeton*.

Przetworzenie elementu z linked list – dopisanie do tablicy lub wybranie do operacji join będzie kosztowało nas jeden żeton przechowywany na elemencie.
Dalej więc do operacji join zawsze będziemy mieli elementy z żetonem na każdym – jednym opłacimy `join`, a drugi pozostawimy na elemencie wynikowym.

Potrzebne nowe żetony:

- nie więcej niż $2\log n$ żetonów, które przypiszemy nowym drzewom po usunięciu minimum
- nie więcej niż $\log n$ żetonów, które umieścimy na drzewach z tablicy zmieniając ją z powrotem w listę.
- nie więcej niż $\log n$ żetonów na wyznaczenie nowego minimum

Złożoność czasowa tej operacji wynosi więc $O(\log n)$.