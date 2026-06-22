Będziemy chcieli zapamiętać $n$ kluczy tak, by:

- wystarczyło pamiętanie $n$ komórek pamięci
- konstrukcja struktury zajmowała czas wielomianowy względem $n$
- czas wykonywania instrukcji `find` był stały

> Nie będzie tutaj operacji `insert` i `delete` – elementy ustalamy na początku.

## Konstrukcja

Będziemy stosowali haszowanie dwupoziomowe.

W pierwszym poziomie funkcja haszująca powinna pozwolić na rozrzucenie kluczy do $n$ kubełków w taki sposób, by $\sum\limits_{i=0}^{n-1}n_{i}^{2} = O(n)$, gdzie $n_{i}$ wyznacza liczbę elementów w $i$-tym kubełku.

W drugim dla każdego kubełka będziemy niezależnie haszować klucze do tablic o wielkości $n_{i}^{2}$.

Do obu poziomów będziemy losowo wybierać funkcje z [[Haszowanie#Funkcje Haszujące|rodziny funkji haszujących]].

**Lemat 1:**
Z prawdopodobieństwem co najmniej $\frac{1}{2}$ funkcja wybrana losowo z [[Haszowanie Uniwersalne|uniwersalnej rodziny haszującej]] rozmieszcza bezkonfliktowo $n = \sqrt{ m }$ kluczy w tablicy $m$ elementowej.
**d-d:**
Dla dowolnych dwóch różnych $x,y$ prawdopodobieństwo, że zachodzi pomiędzy nimi kolizja funkcji haszujących wynosi $\frac{1}{m} = \frac{1}{n^{2}}$ (definicja rodziny uniwersalnej). Jest to również oczekiwana liczba kolizji dla dwóch takich kluczy $x,y$.
Teraz z liniowości [[Wartość Oczekiwana|wartości oczekiwanej]] otrzymujemy, że wartość oczekiwana na liczbę wszystkich kolizji wynosi:
$$
\sum\limits_{x\ne y} \frac{1}{n^{2}} = \binom{n}{2} \frac{1}{n^{2}} < \frac{1}{2}
$$
Dalej możemy wykonać przekształcenia z [[Nierówność Markowa|nierówności Markowa]]:
$$
\begin{align*}
P(X \ge 1) &\le \frac{E(X)}{1} \\
P(X \ge 1) &< \frac{1}{2} \implies P(X = 0) > \frac{1}{2}
\end{align*}
$$

**Lemat 2:**
Jeśli do umieszczania $n$ kluczy w tablicy $n$ elementowej użyjemy losowo wybranej funkcji z rodziny uniwersalnej, to z prawdopodobieństwem co najmniej $\frac{1}{2}$ zachodzi:
$$
\sum\limits_{j=0}^{n-1} n_{j}^{2} < 4n
$$
Gdzie $n_{j}$ oznacza liczbę kluczy umieszczonych w $j$-tym kubełku.
**d-d:**
Najpierw pokażemy, że *wartość oczekiwana* tej sumy jest mniejsza niż $2n$, a później zastosujemy nierówność Markova.

- $E\left( \sum\limits_{j=0}^{n-1}n_{j} \right) = n$, bo po prostu zliczamy wszystkie elementy
- $E\left( \sum\limits_{j=0}^{n-1}\binom{n_{j}}{2} \right)$ wyznacza wartość oczekiwaną wszystkich kolizji. Ponieważ każda para kluczy koliduje z prawdopodobieństwem nie większy, niż $\frac{1}{n}, n=m$, to wnioskujemy, że liczba kolizji jest nie większa niż $\binom{n}{2} \cdot \frac{1}{n} = \frac{n-1}{2}$.

> W drugim punkcie intuicyjnie, jeżeli do jednego kubełka trafiło wiele kluczy to łącznie kolizji jest tyle ile da się utworzyć w nim unikatowych par.

Te równości pozwalają na wykonanie dalszych przekształceń:
$$
\begin{align*}
E\left( \sum\limits_{j=0}^{n-1}\binom{n_{j}}{2} \right) &= E\left( \sum\limits_{j=0}^{n-1} \frac{n_{j}^{2} - n_{j}}{2} \right) \\
E\left( \sum\limits_{j=0}^{n-1}n_{j}^{2} \right) &= 2E\left( \sum\limits_{j=0}^{n-1}\binom{n_{j}}{2} \right) + E\left( \sum\limits_{j=0}^{n-1}n_{j} \right) \le 2\frac{n-1}{2} + n < 2n
\end{align*}
$$
Stąd dalej wykonujemy przekształcenie z nierówności Markowa:
$$
\begin{align*}
P(X \ge 4n) &\le \frac{E(X)}{4n} \\
P(X \ge 4n) &< \frac{1}{2} \implies P(X <4n) \ge \frac{1}{2}
\end{align*}
$$

### Podsumowanie

Ile potrzeba pamięci?

- Nie więcej niż $4n$ komórek w tablicach *wtórnych*
- Trzy komórki na parametry funkcji *pierwotnej* (jedną na $p$, drugą na $a$ i trzecią na $b$)
- Dodatkowo na każdą tablicę *wtórną* pamiętamy po trzy komórki (rozmiar i parametry haszowania)

Czas tworzenia struktury:

-  Mamy prawdopodobieństwo $\frac{1}{2}$ na *dobry* podział $n$ elementów na $n$ kubełków (lemat 2), stąd da się to zrobić liniowo (bo oczekujemy, że za drugim razem się uda)
	- Oczekiwana złożoność tego kroku to $O(n)$
- Mamy prawdopodobieństwo $\frac{1}{2}$ na rozdzielenie $n$ elementów na $n^{2}$ kubełków bez kolizji, stąd oczekujemy, że co najwyżej dwukrotnie trzeba będzie to wykonać
	- Oczekiwana złożoność tego kroku to $O\left( \sum\limits_{i=1}^{n}2n_{i}^{2} \right) = O(n)$

Czas instrukcji find jest stały, bo wystarczy policzyć dwa hasze.

