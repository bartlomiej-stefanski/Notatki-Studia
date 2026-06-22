**Dane:**
Dane są elementy $S$ będące podzbiorem $U$ oraz tablica $T[0\dots|S|-1]$.

**Zadanie:**
Utworzyć funkcję $h: U  \to \{0,\dots m-1\}$ wyznaczającą pozycję odpowiadające elementom $S$ w tablicy $T$.

## Funkcje Haszujące

### Dobra Funkcja Haszująca

Dobra funkcja haszująca powinna spełniać następujący warunek:
$$
\begin{align*}
\forall_{j\in\{0,\dots,m-1\}}\sum\limits_{k\ :\ h(k) = j} P(k) = \frac{1}{m} &&(DFH)
\end{align*}
$$
Czyli chcielibyśmy, by suma prawdopodobieństw [[Przestrzeń Probabilistyczna#Prawdopodobieństwo|prawdopodobieństwo]] mapowań elementów z $U$ na wybrane $j$ wynosiła $\frac{1}{m}$ dla każdego $j$.  
W praktyce warunku tego nie możemy sprawdzać, bo prawie zawsze $P$ nie jest znane oraz chcielibyśmy, by funkcja haszująca działała szybko.

### Przykłady Funkcji Haszujących

$$
h(k) = k \text{ mod } m
$$
Tutaj należy być odrobinę ostrożnym przy wyborze $m$. Jeżeli weźmiemy $m = 2^{p}$, to $h$ wybiera tak naprawdę $p$ ostatnich bitów liczby, których rozkład nie musi być jednorodny. Podobnie dla innych potęg.  
Z tego powodu zaleca się wybieranie $m$ będącego liczbą pierwszą daleką od potęg dwójki.

$$
h(k) = \lfloor m(kA - \lfloor kA \rfloor ) \rfloor 
$$
Tym razem liczba $m$ nie ma dużego wpływu na jakość haszowania, stąd bierze się zwykle potęgę dwójki. Wybór $A$ jest ważniejszy, ale należy go dostosować do danych. Standardowym wyborem może być $A = \frac{\sqrt{ 5 } - 1}{2} \approx 0.6180339887$.

## Metody Pamiętania Elementów

Jeśli mielibyśmy idealną funkcję haszującą, to nie było by tutaj nic do powiedzenia, bo każdy element był by mapowany bezpośrednio na pozycję w tablicy.

Tak jednak w praktyce nie będzie, więc musimy potrafić radzić sobie z sytuacjami, gdzie mamy $x,y\in U$ oraz $h(x) = h(y)$.
Sytuację, gdzie funkcja haszująca dla dwóch elementów wskazuje to samo miejsce w tablicy nazywamy *konfliktem*.

### Listy Elementów

W $i$-tym elemencie tablicy $T$ będziemy przechowywali listy elementów dla których $h(x) = i$. Najczęściej wykorzystamy listę łączoną.

Jeżeli założymy, że wartość funkcji haszującej liczymy w czasie stałym, to koszt operacji `SEARCH` będzie proporcjonalny do długości listy dla tego elementu.

Jeżeli wybierzemy funkcję haszującą spełniającą $(DFH)$, to w łatwy sposób możemy policzyć, że *średni* (oczekiwany) koszt operacji `SEARCH` wynosi $\Theta\left( 1 + \frac{n}{m} \right)$, gdzie $n$ wyznacza liczbę elementów uniwersum $U$ pamiętanych w $T$.

Wartość $\frac{n}{m} = \alpha$ nazywamy *współczynnikiem wypełnienia tablicy*.

**Wniosek:**  
Jeżeli $n = O(m)$, to średni koszt operacji `SEARCH` jest stały.

### Adresowanie Otwarte

Tym razem do haszowania użyjemy rozbudowanej definicji funkcji haszującej:
$$
h: U \times \{0,1,\dots,m-1\} \to \{0,1,\dots,m-1\}
$$
Dodatkowo chcemy, by
$$
\begin{align*}
\forall_{k\in U}\langle h(k, 0), \dots, h(k, m-1)\rangle \text{ było permutacją zbioru } \{0,1,\dots,m-1\} && (PER)
\end{align*}
$$

Wtedy faktycznie do przechowywania wystarczy $m$-elementowa tablica wartości $T$.  
Wstawianie elementu zaczniemy od próby $h(k, 0)$, jeżeli to się nie powiedzie to będziemy przechodzić po kolejnych $h(k, i)$ aż do wstawienia elementu, albo zweryfikowania, że nie można wstawić kolejnego elementu, bo tablica haszująca jest pełna.

#### Metody

##### Metoda Liniowa

$$
h(k, i) = (h'(k) + i) \text{ mod } m
$$
gdzie $h'$ jest *standardową* funkcją haszującą. Warunek $(PER)$ mamy za darmo.

##### Metoda Kwadratowa

$$
h(k, i) = (h'(k) + c_{1}i + c_{2}i^{2}) \text{ mod } m
$$
gdzie $h'$ tak jak poprzednio.
Dodatkowo $c_{1},c_{2} \ne 0$ oraz należy dobrać je razem z $m$ tak, by zachodziło $(PER)$.

##### Podwójne Haszowanie

$$
h(k, i) = (h'(k) + ih''(k)) \text{ mod }
$$
gdzie $h',h''$ pomocnicze funkcje haszujące.
By spełnić $(PER)$ potrzebujemy, by $h''(k)$ było względnie pierwsze z $m$.

> W praktyce najlepsze rezultaty daje haszowanie podwójne.
> Metoda liniowa i kwadratowa sprzyjają koncentrowaniu elementów w 'zlepki' – obszary tablicy $T$ ze znacznie większą gęstością zajętych miejsc.

#### Analiza Kosztów

Dla uproszczenia przyjmiemy wyidealizowane założenie, że:
$$
\begin{align*}
(DPER) \\
\langle h(k,0), \dots, h(k, m-1)\rangle \text{ jest równie prawdopodobnie dowolną permutacją } \{0, \dots, m- 1\}
\end{align*}
$$

**Twierdzenie 1:**  
Przy założeniu $(DPER)$ – doskonałych permutacji i $\alpha = \frac{n}{m}  < 1$ oczekiwana liczba prób wyszukiwania miejsca dla nowego $k$ jest nie większy niż $\frac{1}{1 - \alpha}$.  
**d-d:**  
Z założenia $(DPER)$ mamy, że $h(k, i)$ z równym prawdopodobieństwem wskazuje każdą pozycję w tablicy oraz wskazywana pozycja jest inna niż poprzednie (bo generujemy permutację).  
Teraz rozpiszmy zmienną losową $X$ przyjmującą wartość najmniejszego $i$ takiego, że $h(k, i)$  nie zostało użyte.  
Inaczej: $P(X \ge z)$ odpowiada prawdopodobieństwu, że potrzeba wykonań co najmniej $z$ instrukcji, stąd intuicyjnie:
$$
\begin{align*}
P(X \ge z) &= \text{"nie udało się w każdej poprzedniej"} \\
&= \frac{n}{m}\cdot \frac{m-1}{m-1} \cdot \dots \cdot \frac{n-z+2}{m-z +2} \\
&\le \left( \frac{n}{m} \right)^{i-1} = \alpha^{i-1}
\end{align*}
$$
Możemy więc wyznaczyć jawny wzór na wartość oczekiwaną pozycji, na której pierwszy raz wyznaczymy nowe miejsce w tablicy:
$$
\begin{align*}
E(X) \overset{(1)}{=} \sum\limits_{i=1}^{\infty}P(X \ge i) \le \sum\limits_{i=1}^{\infty}\alpha^{i-1} = \frac{1}{1 - \alpha}
\end{align*}
$$
$(1)$ Dowód przejścia [[Wartość Oczekiwana#Alternatywny Wzór Dla Dziedziny Naturalnej|tutaj]].

**Twierdzenie 2:**  
Przy założeniu $(DPER)$ oczekiwany czas wyszukiwania elementu zawartego w tablicy zapełnionej ze współczynnikiem $\alpha = \frac{n}{m} < 1$ jest nie większy niż $\frac{1}{\alpha}\ln \frac{1}{1-\alpha}$.  
**d-d:**  
Jeżeli teraz w tablicy jest $n$ elementów, to z równym prawdopodobieństwem będziemy próbowali wyszukać element wstawiony kiedy w tablicy było $i\in\{0, \dots, n-1\}$ elementów. Weźmiemy więc średnią oszacowań z twierdzenia pierwszego:
$$
\begin{align*}
\frac{1}{n}\sum\limits_{i=0}^{n-1} \frac{1}{1-\frac{i}{m}} &= \frac{1}{n}\sum\limits_{i=0}^{n-1} \frac{m}{m-i} \\
&= \frac{m}{n} \sum\limits_{i=0}^{n-1} \frac{1}{m-i} \\
&= \frac{1}{\alpha} \sum\limits_{j = m - n + 1}^{m} \frac{1}{j} \\
&\le \frac{1}{\alpha} \int_{m-n}^{m} \frac{1}{x}dx \\
&= \frac{1}{\alpha} \left . \ln x \right|_{m - n}^{m} \\
&= \frac{1}{\alpha} \ln \frac{m}{m-n} \\
&= \frac{1}{\alpha}\ln \frac{1}{1-\alpha}
\end{align*}
$$
Przejście do całki jest standardowym oszacowaniem przy interpretacji funkcji jako 'słupki'.