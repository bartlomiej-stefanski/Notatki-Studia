Co jeżeli chcemy zbudować [[Zbalansowane Drzewa|zbalansowane drzewo]], ale nie chcemy zajmować się jakimiś skomplikowanymi niezmiennikami z AVL?
Wtedy budujemy drzewa czerwono-czarne!

> Nie wiem czy to jest mniej skomplikowane niż zwykłe [[Drzewa AVL|AVL]]...

[[Binary Search Tree|Binarne drzewo przeszukiwań]] jest drzewem czerwono-czarnym tylko jeśli:

1. Każdy wierzchołek jest czerwony lub czarny
2. Każdy liść jest czarny
3. Jeśli wierzchołek jest czerwony, to obaj jego synowie są czarni
4. Na każdej ścieżce prowadzącej z danego wierzchołka do liścia jest jednakowa liczba czarnych wierzchołków

> Intuicyjnie wierzchołki czerwone będą *nadmiarowe, psujące balans*. Poprzez definicję drzewa zapewniamy jednak, że nie więcej niż co drugi wierzchołek jest *psujący*.

***Def:***
Liczbę czarnych wierzchołków na ścieżce od wierzchołka $x$ do liścia będziemy oznaczać $bh(x)$.

**Twierdzenie:**
Czarno-czerwone drzewo o $n$ wierzchołkach wewnętrznych ma wysokość nie większą niż $2\log(n+1)$.
**d-d:**
Najpierw zauważmy, że jeżeli dla pewnego wierzchołka $x$ mamy $bh(x)$ czarnych wierzchołków na drodze do korzenia, to całkowita wysokość drzewa jest nie większa niż $2bh(x)$, bo dwa czerwone wierzchołki nie mogą wystąpić pod rząd.
Teraz określmy liczbę wierzchołków w drzewie o wysokości $bh(x)$. Oczywiście dla $bh(x) = 2$ mamy minimalnie jeden wierzchołek (ten wierzchołek i dwa czarne liście). Indukcyjnie załóżmy, że dla $bh(x) < k$ mamy co najmniej $2^{bh(x) - 1}$ wierzchołków.
Pokażmy, że implikuje to tezę dla $k$:
Jeżeli mamy $bh(x) = k$, to drzewo składa się z przynajmniej  jednego wierzchołka czarnego $c$ dla którego $bh(c) = k$, a ten wierzchołek ma z kolei dwa poddrzewa, które z indukcji mają nie mniej niż $2^{(k-1) - 1}$ wierzchołków. Łącznie drzewo będzie mieć nie mniej niż:
$$
1 + 2(2^{(k-1) - 1} - 1) = 2^{k - 1} - 1
$$
Co dowodzi tezy dla $bh(x) = k$. Na mocy indukcji .......
Pozostaje jedynie wnioskowanie o wysokości drzewa, co robimy poprzez określenie minimalnej liczby wierzchołków co robimy naturalnie poprzez wzięcie logarytmu: $bh(x) \le \log(n + 1)$ no i stąd wnioskowanie na prawdziwą wysokość $h \le 2 \log(n+1)$

## Operacje Słownikowe

Find jest nie ciekawe, bo przebiega zupełnie standardowo.
Gorzej będzie z innymi operacjami, gdzie trzeba będzie naprawiać własności drzewa.

### Insert

Wstawianie przeprowadzamy jak dla *standardowego* drzewa przeszukiwań binarnych. Nowy wierzchołek kolorujemy na czerwono i ustawiamy synów na liście (które są czarne).

Po tej operacji jedyną własnością, którą mogliśmy zaburzyć jest $(3)$.

#### Naprawa Zaburzenia (3)

Poniżej zawarte są rozważania przypadków dla czerwonego elementu $x$. Poprzez $P,G,U$ będą oznaczeni odpowiednio jego rodzic (parent), dziadek (grandparent) i wujek (uncle).
Zakładam, że $P$ jest lewym synem $G$, kiedy $G$ musi istnieć. Jeżeli by tak nie było, to postępujemy symetrycznie.

##### 1

$P$ jest czarny -> kończymy

##### 2

Jeżeli zarówno $P,U$ są czerwone, ale $G$ jest czarny, to $P,U$ można zmienić na kolor czarny, a $G$ na czerwony. Zachowujemy tym samym warunek $(4)$, ale trzeba ponownie sprawdzić, czy $G$ spełnia warunek $(3)$ (no i być może naprawić).
![[Drzewa-czerwono-czarne-case2.png|400]]

##### 3

$P$ jest czerwonym korzeniem – możemy zmienić go na kolor czarny, a wtedy własności będą zachowane. Podnosi to jednak wysokość $bh$ drzewa.

##### 4

$P$ jest czerwony, ale $U$ i $G$ są czarne. Wierzchołek $x$ jest **prawym** synem $P$.
Wykonujemy rotację dla $P$ i $x$. Wtedy miejsce $P$ zajmie element $x$, a $P$ będzie lewym synem $x$.
Teraz musimy naprawić $P$ i to z nim przejdziemy do przypadku `5`.
![[Drzewo-czarno-czerwone-case4.png|400]]

##### 5

$P$ jest czerwony, ale $U$ i $G$ są czarne. Wierzchołek $x$ jest **lewym** synem $P$.
Wykonamy teraz rotację dla $P$ i $G$, która umieści $P$ w miejsce $G$, który z kolei stanie się prawym synem $P$.
Teraz zauważamy, że by naprawić kolorowanie wystarczy *spropagować* czerwony kolor z $P$ do $G$, a drzewo zostanie zachowane. Nie zmieniliśmy struktury *na zewnątrz*, więc nie ma konieczności dalszych napraw.
![[Drzewa-czerwono-czarne-case5.png|400]]

### Delete

Wykonujemy *początkowo* tak jak w drzewie AVL, więc usuwamy wierzchołek tylko bez następników, lub z jednym następnikiem. Jeżeli usuwany wierzchołek jest czerwony, to nie ma on dzieci (łatwe do pokazania), więc jest to trywialne.
Gorzej, gdy usuwany wierzchołek jest czarny...

Ideą rozwiązania będzie wyobrażenie sobie, że z usuwanego wierzchołka przenosimy kolor czarny na syna którym zastąpimy usuwany wierzchołek. Jeżeli syn był czerwony, to wszystko działa, ale jeżeli nie być (czyli zastąpiliśmy element liściem), to ten liść jest teraz *podwójnie czarny* – musi taki być, by spełniony był niezmiennik $(4)$.
Ten nadmiarowy czarny kolor będziemy przepychać do góry aż znajdziemy czerwony wierzchołek, gdzie możemy go umieścić, lub aż do dotarcia do korzenia.

#### Naprawa Własności (4)

Analizujemy z perspektywy wierzchołka $x$ z podwójnym kolorem czarnym. Dodatkowo zakładamy, że $x$ jest lewym synem (dla prawego syna rozważania są symetryczne).

##### 1

Brat $x$ jest czerwony (więc ojciec jest czarny).
Wtedy brata kolorujemy na czarno, a ojca na czerwono.
dalej wykonujemy rotację na ojcu i bracie $x$. Ta transformacja zaprowadzi nas do jednego z innych przypadków.

##### 2

Brat $x$ jest czarny i obydwaj bratankowie są czarni.

- Malujemy brata na czerwono
- Przesuwamy ekstra kolor czarny na ojca $x$

Wtedy oba poddrzewa ojca $x$ mają takie same $bh$. Dalej być może trzeba naprawić ojca...

##### 3

Brat $x$ jest czarny, lewy bratanek czerwony, a prawy czarny.

- Malujemy brata na czerwono i lewego bratanka na czarno. 
- Wykonujemy rotację dla brata i jego lewego syna (nowym bratem $x$ jest lewy bratanek)

Otrzymujemy przypadek `4`

##### 4

Brat $x$ jest czarny, a prawy bratanek czerwony.

- Malujemy brata $x$ na kolor ojca $x$
- Ojca $x$ malujemy na czarno
- Prawego bratanka malujemy na czarno (extra kolor z $x$)
- Wykonujemy rotację dla ojca i brata. Dziadkiem zostaje ówczesny brat.


### Analiza Kosztów

Wszystkie naprawy własności wykonują się w czasie stałym. Napraw wykonamy co najwyżej $h$ wiele. Reszta operacji jak w standardowym $h$.
