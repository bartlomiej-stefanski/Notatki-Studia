**Dane:**
Ciąg elementów $T[1\dots n]$ z porządkiem liniowym.

> Zakładamy bez straty ogólności, że liczby są różne.

**Zadanie:**
Znaleźć $k$-tą liczbę w kolejności według danego porządku.

Będziemy chcieli z ciągu elementów $T$ wybrać losowo dosyć małą próbkę $R$, ale na tyle dużą, by była spora szansa na to, że zawiera ona odpowiednio wiele informacji, by później odnaleźć medianę.
Z próbki $R$ wyznaczamy *znaczniki* $L,H$ dla których istnieje spora szansa na to, że:

- mediana zawarta jest pomiędzy $L,H$
- liczba elementów $T$ zawartych w przedziale $[L,H]$ jest *mała*

Jeżeli faktycznie tak jest, to elementy z tego przedziału sortujemy i od razu wyznaczamy medianę.

##### Algorytm

Poniżej znajduje się algorytm realizujący ta metodę z już dobranymi odpowiednio stałymi:

1. Wybierz losowo, *z powtórzeniami* próbkę $R$ złożoną z $n^{3/4}$ elementów.
2. Posortuj $R$
3. $x = kn^{-1/4}, l = \max\{\lfloor x - \sqrt{ n } \rfloor, 1\}, h = \min\{\lfloor x - \sqrt{ n } \rfloor, n^{3/4}\}$
	1. $L = R[l]$
	2. $H = R[h]$
4. Wyznacz liczbę elementów ($C_{l}$) mniejszych niż $L$ oraz zbiór elementów $P$ zawartych w przedziale $[L,H]$, dalej sprawdź czy:
	1. $k$-ty element znajduje się w $P$ – czy $C_{l} < k \le |P| + C_{l}$
	2. zbiór $P$ jest odpowiednio mały: $|P| \le 4n^{3/4} + 2$
		- Jeśli `4.1` lub `4.2` nie zachodzi, to wróć do `1`
5. Posortuj $P$, a następnie wybierz oczekiwany element.

### Złożoność Obliczeniowa

**Lemat:**
Z prawdopodobieństwem $1 - O\left( n^{-1/4} \right)$ algorytm potrzebuje tylko jednej iteracji.

**d-d:**
1. Pokazujemy, że $kn^{-1/4}$ jest wartością oczekiwaną liczby elementów mniejszych niż $k$-ty w $R$
2. Pokazujemy, że wariancja tej zmiennej losowej jest mniejsza niż $\sqrt{ n }$
3. Korzystamy z [[Nierówność Czebyszewa|nierówności Czebyszewa]]

> Jeżeli uwierzymy, że zachodzi $1,2$, to intuicyjnie wybieramy *przedział ufności*, do którego *często* trafią wyniki pomiarów próbek oraz te które tam trafią będziemy potrafili łatwo procesować.

#TODO  Uzupełnić dowód na podstawie *R.Motwani, P.Raghavan, Randomized Algorithms*.

> Dowód tego lematu ponoć wykracza poza zakres wykładu.
