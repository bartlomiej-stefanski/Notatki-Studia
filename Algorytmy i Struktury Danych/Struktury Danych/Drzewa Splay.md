Jest to samoorganizujące się drzewo binarne – podczas wykonywania standardowych operacji będzie *automatycznie* zmieniać swoją strukturę stosując pewną heurystykę.
Dla drzew splay, w przeciwieństwie do drzew zbalansowanych (AVL, czerwono-czarnych) nie będziemy potrzebowali żadnych dodatkowych informacji w wierzchołkach.

Heurystyka którą tutaj zastosujemy nie będzie dawała ścisłych ograniczeń na koszt pojedynczych operacji na drzewie, ale okaże się, że koszt zamortyzowany jest niski.

## Operacje na Drzewach Samoorganizujących Się

Oprócz standardowych operacji słownikowych `find(i, S)`, `insert(i, S)`, `delete(i, S)` dostępne są operacje:

- $\text{join}(S_{1},S_{2})$ – połącz drzewa $S_{1}$ i $S_{2}$ w jedno drzewo zakładają, że każdy klucz w drzewie $S_{1}$ jest nie większy od każdego kluczu w drzewie $S_{2}$
- $\text{split}(i, S)$ – rozdziel $S$ na drzewa $S_{1},S_{2}$ takie, że każdy klucz w $S_{1}$ jest nie większy niż $i$, a każdy klucz w $S_{2}$ jest nie mniejszy niż $i$

## Implementacja Operacji

Podstawowa idea drzew samoorganizujących się polega na tym, by wierzchołki drzewa zawierające klucz $i$ przesuwać rotacjami do korzenia.
Jeżeli wybierzemy *fajne* rotacje do wykonania, to przy okazji poprawimy strukturę drzewa.

By implementacja pozostałych operacji była *wygodna* zdefiniujemy operację:

- $\text{splay}(j, S)$ – przeorganizuj $S$ tak, by jego korzeniem stał się wierzchołek zawierający $k$ takie, że w $S$ nie ma elementu leżącego między $k$ i $j$.

> Jeżeli $j\in S$ , to wierzchołek $j$ zostanie przesunięty do korzenia.

### Implementacja Splay

Najprostszym wariantem jest wykonanie rotacji aż dotrzemy z wierzchołkiem do korzenia. Takie rozwiązanie będzie działać, ale łatwo wyznaczyć ciąg $n$ operacji, których koszt wyniesie $O(n^{2})$, a na koniec struktura drzewa będzie taka jak wcześniej (słabo trochę).

Stad potrzebny jest lepszy sposób.
Będziemy w nim rozpatrywać trzy przypadki:

**1. x nie ma dziadka:**

Dla wierzchołka `x` i jego rodzica `y` wykonujemy `rotate(x,y)`

**2. x jest lewym synem ojca, a ojciec y jest lewym synem dziadka x:**

- `rotate(y, p(y))`
- `rotate(x, y)`

**3. Pozostałe przypadki:**

Dla wierzchołka `x` i jego ojca `p(x)`:

- `rotate(x, p(x))`
- `rotate(x, p(x))`

#### Analiza Kosztu Splay (zamortyzowana)

Każdy wierzchołek przechowuje pewien depozyt, operacje na drzewie zwiększają ten depozyt lub korzystają z niego.

Oznaczenia do analizy:

- $S(x)$ – poddrzewo o korzeniu w $x$
- $|S|$ – liczba wierzchołków w drzewie $S$
- $\mu(S) = \lfloor \log(|S|) \rfloor$ – hipotetyczna wysokość drzewa $S$
- $\mu(x) = \mu(S(x))$ – hipotetyczna wysokość poddrzewa ukorzenionego w $x$

Teraz będziemy utrzymywać następujący niezmiennik:
$$
\text{Wierzchołek x ma zawsze co najmniej } \mu(x) \text{ jednostek na swoim koncie.}
$$
Ustalamy również, że `insert` daje wierzchołkowi pewien początkowy depozyt.

##### **Lemat:**

Każda operacja $\text{Splay}(x,S)$ wymaga nie więcej niż $3(\mu(S) - \mu(x)) +1$ jednostek do wykonania operacji i zachowania niezmiennika kredytowego.

##### **d-d:**

Rozważmy wszystkie możliwe przypadki zamian dla wierzchołków $x,y,z$, gdzie $y$ jest ojcem $x$, a $z$ jest ojcem $y$. Dodatkowo niech $\mu,\mu'$ oznaczają *depozyty* w wierzchołkach przed i po wykonaniu operacji.

###### 1. z nie istnieje:
![[splay-tree-analysis1.png]]
Widzimy, że zmianie mogła ulec jedynie wysokość `x` i `y`, więc zapłacić będziemy musieli:
$$
\mu'(x) + \mu'(y) - \mu(x) - \mu(y)
$$
Wcześniej zauważamy jednak, że zachodzi:

- $\mu'(x) = \mu(y)$
- $\mu'(x) \ge \mu(x)$
- $\mu'(y) \le \mu'(x)$

Stad za wykonane zmiany musimy więc zapłacić:
$$
\mu'(x) + \mu'(y) - \mu(x) - \mu(y) = \mu'(y) - \mu(x) \le \mu'(x) - \mu(x) \le 3(\mu'(x) - \mu(x))
$$
Jesteśmy więc w stanie opłacić te operacje, a dodatkowo zostanie nam jednostka na opłacenie niskopoziomowych operacji, które wykonamy.

###### 2. y jest lewym synem i x jest lewym synem:
![[splay-tree-analysis2.png]]
Jedynie poddrzewa ukorzenione w `x`, `y` i `z` mogły zmienić swoją wysokość, więc by utrzymać niezmiennik potrzebujemy zużyć następującą liczbę żetonów:
$$
\mu'(x) + \mu'(y) + \mu'(z) - \mu(x) - \mu(y) - \mu(z) = (*)
$$
Zauważamy, że po wykonaniu rotacji $\mu'(x) = \mu(z)$m skąd dalej:
$$
\begin{align*}
(*) = \mu'(y) + \mu'(z) - \mu(x) - \mu(y) &= [\mu'(y) - \mu(x)] + [\mu'(z) - \mu(y)] \\
&\le[\mu'(x) - \mu(x)] + [\mu'(x) - \mu(x)] \\
&\le 2[\mu'(x) - \mu(x)]
\end{align*}
$$
Zostanie więc $\mu'(x) - \mu(x)$ żetonów na opłacenie operacji niskiego poziomu, jednak czy będzie to wystarczająca ilość?
Okazuje się, że tak, bo ta suma jest dodatnia, lub jeżeli jest zerowa, to zmniejszą się wymagane depozyty w innych wierzchołka i to z nich weźmiemy żetony potrzebne do wykonania operacji.

**Fakt:**
Jeżeli $\mu'(x) = \mu(x)$, to zachodzi $(*) < 0$.
**d-d:**
Ponieważ $\mu(x) \le \mu(y) \le \mu(z) = \mu'(x) = \mu(x)$ otrzymujemy równość $\mu(x) = \mu(y) = \mu(z)$.

Dalej załóżmy nie wprost, że jeśli $\mu'(x) = \mu(x)$, to $\mu'(x) + \mu'(y) + \mu'(z) \ge \mu(x) + \mu(y) + \mu(z)$.
Z tego otrzymujemy, że:
$$
\mu'(x) + \mu'(y) + \mu'(z) \ge 3\mu(x) = 3\mu'(x)
$$
Dalej zauważamy, że wartości $\mu'(y),\mu'(z)$ nie mogą być ujemne oraz są nie większe niż $\mu'(x)$, więc zachodzi:
$$
\begin{align*}
\mu'(x) = \mu'&(y) = \mu'(z) \\
&\Downarrow \\
\mu(x) = \mu(y) = \mu(z) &= \mu'(x) = \mu'(y) = \mu'(z) &&(1)
\end{align*}
$$
Zauważamy teraz (rysunek), że poddrzewa początkowo podpięte do $x$ są różne względem tych, które zostaną podpięte pod $z$. Oznaczmy moce zbiorów tych poddrzew jako odpowiednio $a,b$. Z równości $(1)$ oczekiwalibyśmy więc, że:
$$
\begin{align*}
\mu(x) = \mu'&(x) = \mu'(z) \\
\lfloor \log a \rfloor = \lfloor \log&(a+ b + 1) \rfloor = \lfloor \log b \rfloor 
\end{align*}
$$
To jednak jest sprzeczne, bo:
$$
\lfloor \log(a + b + 1) \rfloor \ge \lfloor \log(2\min\{a,b\}) \rfloor > \lfloor \log(\min\{a,b\}) \rfloor   
$$

###### 3. x jest lewym synem, a y prawym

Analizujemy identycznie co przypadek `2`.

##### Podsumowanie

Pokazaliśmy, że każdy przypadek wymaga nie więcej niż $3(\mu'(x) - \mu(x))$ żetonów do przetworzenia.
W trakcie operacji `splay` będziemy przesuwać wierzchołek $x$ coraz wyżej na kolejne pozycje $S_{1},S_{2},\dots,S_{k}$. Każde z tych przesunięć będzie jednym z rozważanych przypadków.
Łącznie będą więc kosztowały:
$$
\begin{align*}
3(\mu(S_{1}) - \mu(x)) &+ 3(\mu(S_{2}) - \mu(S_{1})) + \dots + 3(\mu(S_{k}) - \mu(S_{k-1})) + 1 =\\
&= 3(\mu(S_{k}) - \mu(x)) +1  \\
&= 3(\mu(S) - \mu(x)) + 1
\end{align*}
$$

#### Złożoność Obliczeniowa Innych Operacji

Zauważamy, że każdą operację można wyrazić jako stała liczba operacji `splay` + dodatkowy processing w czasie stałym, to wnioskujemy, że koszt tych operacji jest asymptotycznie równy kosztowi operacji `splay`.

Z tego, że wartość $\mu$ nie przekracza $\log n$ w drzewie $n$ wierzchołkowym wnioskujemy, że operacje działają w czasie logarytmicznym.

> Operacja `insert` również – potrzebuje przejść po drzewie oraz odłożyć nie więcej niż $\log n$ żetonów na nowy wierzchołek.

**Twierdzenie:**
Łączny koszt ciągu $m$ operacji na drzewie zawierającym $n$ wierzchołków wynosi $m\log n$.
**d-d:**
> Z lematu i złożoności operacji.
 