## Alfabet

Zbiór $\sum$ symboli używanych do budowy słów:

- $\sum = \set{0, 1} = B$ — Alfabet binarny
- $\sum = \set{a,b,\dots , z}$ — Alfabet małych znaków łacińskich

## Słowo

Ciąg znaków nad wybranym alfabetem $\sum$; np.:
- 1, 101, 1111 — Słowa nad alfabetem binarnym
- a, abab, qwerty — Słowa nad alfabetem znaków łacińskich

#### Długość Słowa

$|w|$ Oznacza liczbę liter w słowie `w`; Przykładowo $|abc| = 3$.

#### Słowo Puste

$\epsilon$ oznacza słowo puste, tzn. Jedyne słowo długości `0`: $|\epsilon|=0$.

#### Konkatenacja Słów

$vw$ Oznacza słowo zbudowane z wszystkich liter słowa $v$, a następnie wszystkich liter słowa $w$; Przykładowo $(abc)(def)=abcdef$.

- Elementem neutralnym konkatenacji jest $\epsilon$
- Konkatenacja jest łączna, ale nie przemienna

#### Potęgowanie Słów

Słowo $w^{n}$ — n-krotne powtórzenie słowa $w$. Przykładowo:

- $a^{0} = \epsilon$
- $(ba)^{2} = baba$

## Gwiazdka Kleene'go

Zbiór $\sum^{*}$ — wszystkie słowa, dowolnej długości nad alfabetem $\sum$:
$${\sum}^{*} = \set{a_{1}a_{2}\dots a_{n} | n \in N \land \forall_{k \in \set{1,\dots,n}}a_{k}\in\sum}$$
Formalnie definiowane jako najmniejszy zbiór spełniający warunki:
$$\epsilon \in {\sum}^{*}$$
$$a \in \sum \land w\in {\sum}^{*} \rightarrow aw \in {\sum}^{*}$$
Przykłady:
- $\set{a}^{*}=\set{\epsilon,a,aa,aaa,\dots}$
- $\set{a,b}^{*}=\set{\epsilon,a,b,aa,ab,ba,bb,\dots}$

## Język

Język nad alfabetem $\sum$ nazywamy dowolny zbiór $L \subseteq \sum^{*}$ .
Przykłady:

- $\set{w0 | w \in B^{*}}$ – zbiór parzystych liczb binarnych
- $\set{w\in B^{*} |\ |w| = n}$ – zbiór ciągów binarnych o długości $n$
- $\set{0^{n}1^{n} | n \in N}$ – zbiór ciągów binarnych zbudowany z konkatenacji bloku zer i bloku jedynek tej samej długości

#### Język Pusty

$\emptyset$ – język nie zawierający żadnego słowa.
To jest coś innego niż $\set{\epsilon}$ – język zawierający jedno puste słowo

#### Potęgowanie Języków

$L^{n}$ – język słów zbudowanych z konkatenacji $n$ słów z $L$:
$$L^{n} = \set{w_{1}w_{2}\dots w_{n} | \forall_{k \in \set{1,\dots,n}}w_{k} \in L}$$
Przykłady:
- $B^{0} = \set{\epsilon}$
- $B^{3} = \set{000,001,010,011,100,101,110,111}$
- $\set{ba,za}^{2} = \set{baba,baza,zaba,zaza}$

#### Singleton

Język zawierający tylko jedno słowo – przykładowo $\set{10}$.

#### Konkatenacja Języków

Język $L_{1}L_{2}$ – zbiór konkatenacji wszystkich słów z $L_{1}$ ze wszystkimi z $L_{2}$:
$$L_{1}L_{2} = \set{w_{1}w_{2} | w_{1} \in L_{1}\land w_{2}\in L_{2}}$$
Na przykład:
- $\emptyset L = L\emptyset = \emptyset$
- $\set{\epsilon}L = L\set{\epsilon} = L$
- $\set{ko,plo}\set{n,za} = \set{kon,koza,plon,ploza}$

#### Suma Języków

Język $L_{1} \bigcup L_{2}$ – zbiór słów, które należą do $L_{1}$ lub $L_{2}$.
Przykład: $\set{0,00} \bigcup \set{1,11} = \set{0,00,1,11}$

#### Gwiazdka Kleene'go Dla Języków

Język $L^{*}$ – zbiór konkatenacji dowolnej liczby słów z $L$:
$$L^{*} = L^{0}\cup L^{1}\cup L^{2}\cup \dots$$

#### Plus Kleene'go Dla Języków

Język $L^{+}$ – zbiór konkatenacji dowolnej liczby słów z $L$:
$$L^{*} = L^{1}\cup L^{2}\cup \dots = LL^{*}$$

## Wyrażenia Regularne

Wyrażenia opisujące języki regularne:

- $L(\emptyset) = \emptyset$
- $L(\epsilon) = \set{\epsilon}$
- $L(a) = \set{a}$
- $L(e_{1} + e_{2}) = L(e_{1}) \cup L(e_{2})$
- $L(e_{1}e_{2}) = L(e_{1})L(e_{2})$
- $L(e^{*}) = L(e)^{*}$
