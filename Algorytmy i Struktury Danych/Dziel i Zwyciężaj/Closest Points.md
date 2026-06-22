**Dane:**
$p_{1},p_{2},\dots,p_{n}\in\mathbb{R}^{2}$ – punkty na płaszczyźnie.

**Zadanie:**
Wyznaczyć $j \ne i$ takie, że odległość (na płaszczyźnie) $p_{i}$ od $p_{j}$ jest najmniejsza.

## Naiwnie

Sprawdzamy każdy punkt z każdym innym.
Zajmie nam to $O(n^{2})$.

## Dziel i Zwyciężaj

> Istnieje algorytm randomizowany o oczekiwanej złożoności $O(n)$ korzystający z [[Haszowanie|haszowania]].

### Strategia

Dla niewielu punktów liczymy minimalną odległość porównując ze sobą wszystkie możliwe pary.
Jeżeli par jest więcej, to wykonujemy:

1. Posortuj wszystkie punkty względem współrzędnych $x$ i zapamiętaj je w tablicy $X$.
2. Posortuj wszystkie punkty względem współrzędnych $y$ i zapamiętaj je w tablicy $Y$.
3. Znajdź *pionową* prostą $l$ rozdzielającą $P$ na dwa równoliczne podzbiory $P_{l}$ i $P_{r}$.
4. Uruchom algorytm rekurencyjnie dla punktów $P_{l},P_{r}$; niech najbliższa znaleziona odległość jest pomiędzy $i',j'$ i wynosi $d$
5. Sprawdź, czy istnieje mniej odległa para pomiędzy zbiorami $P_{l}$ i $P_{r}$:
	1. Wyznacz na podstawie $Y, P_{l},P_{r}$ sekwencję $P_{c}$ punktów odległych od $l$ o nie więcej niż $d$.
	2. Przechodząc *gąsienicowo* po wysokości porównaj odległości pomiędzy punktami (jeżeli któraś jest lepsza, to mamy nowe $d$)

### Uzasadnienie

Dla każdej prostej $l$ rozdzielającej punkty najbliższa para jest na lewo, prawo, lub *pomiędzy*. Sprawdzamy wszystkie możliwości, więc znajdziemy minimalną odległościowo parę.

### Złożoność Obliczeniowa

Najpierw pokażmy, że *gąsienicowe przejście* zajmuje liniowo wiele czasu – każdy punkt porównamy z co najwyżej stałą liczbą innych:

Dla danego punktu $p$ potencjalni kandydaci na *najbliższy punkt* będą znajdowali się w prostokącie o wysokości $d$ i szerokości $2d$.
Tak, by w żadnej połówce nie znajdowała się para punktów bliższa niż $d$ możemy umieścić w każdej co najwyżej trzy punkty (jako trójkąt równoboczny).
Będziemy mieli więc co najwyżej $5$ innych punktów do porównania odległości – jest ich $O(1)$.

To pozwala już rozpisać równanie rekurencyjne na złożoność obliczeniową:
$$
T(n) = 2T\left( \frac{n}{2} \right) + \Theta(n \log n) = \Theta(n \log^{2}n )
$$
Rozdzielanie danych wymaga sortowania stąd $n \log n$.

> Jeżeli pozbędziemy się sortowania (co jest dosyć łatwe), to można zredukować czas działania do $O(n \log n)$.
> Kopiowania tablic też można się pozbyć.

