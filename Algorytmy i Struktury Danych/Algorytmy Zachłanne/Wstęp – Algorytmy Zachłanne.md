Typowe zadanie rozwiązywane metodą zachłanną ma charakter optymalizacyjny. Mamy skończony zbiór $C$, rozwiązaniami są pewne podzbiory zbioru $C$.
Znane jest kryterium pozwalające na ocenę potencjalnych rozwiązań. Chcemy wybrać rozwiązanie najlepsze względem tego kryterium.

Algorytm zachłanny konstruuje rozwiązanie $S$ stopniowo, zazwyczaj startując od zbioru pustego.
W kolejnych iteracjach algorytm rozważa jeden element $x\in C$. Jeżeli $S\cup \{x\}$ prowadzi do rozwiązania to $x$ zostanie dodane do $S$. Niezależnie od decyzji $x$ usuwany jest z $C$ (nie rozpatrujemy elementów wielokrotnie).
Sam wybór elementu $x$ dokonywany jest na podstawie lokalnego (*zachłannego*) kryterium.

Algorytmy zachłanne nie podejmują żadnych działań sprawdzających, czy konstruowany zbiór może prowadzić do optymalnego rozwiązania.
Oznacza to, że taki algorytm ***nie zawsze*** będzie prowadził do rozwiązania optymalnego (albo w ogóle żadnego poprawnego!), choć często będzie dosyć prosty.
Konieczna jest więc analiza poprawności takiego algorytmu, ale nawet algorytm nieoptymalny może okazać się przydatny jeżeli rozwiązania będą *tylko trochę* nie optymalne.

## Przykład

**Dane:**
Liczba naturalna $R$ oraz zbiór liczb naturalnych $c_{1},c_{2},\dots,c_{k}$.

> Można interpretować, że $R$ jest resztą, a $c_{i}$ są monetami.

**Zadanie:**
Wydać kwotę $R$, możliwie najmniejszą liczbą monet (jeżeli dysponujemy nieskończoną liczbą monet).

### Interpretacja Zachłanna

W tym zadaniu mamy zbiór monet $C$, a potencjalnymi rozwiązaniami będą jego podzbiory.
Poprawnymi rozwiązaniami będą podzbiory, których elementy sumują się do $R$.
Kryterium oceny rozwiązania będzie wielkość podzbioru (chcemy użyć minimalnej ilości monet).

#### Możliwa Strategia Zachłanna

Zaczynając od pustego zbioru wydanych monet będziemy dodawać do rozwiązania największą monetę, która nie spowoduje przekroczenia $R$.

#### Sprawdzenie Poprawności

Ta strategia nie zawsze działa. Zależne jest to od zbioru monet którym dysponujemy – z tego powodu ważne jest przeprowadzenie dowodu.

Co ważne dotyczy to nie tylko optymalności, ale również *ogólnie* tworzenia poprawnych rozwiązań.

##### Niepoprawne Działanie 

- $C = \{1, 3, 4\}$ prowadzi do wydania kwoty $6$ jako $4 + 1 + 1$ zamiast $3 + 3$.
- $C = \{3, 4\}$ prowadzi do porażki przy próbie wydania kwoty $6$ (mimo że się da).

W takich przypadkach najłatwiej poszukać kontrprzykładu.

##### Poprawne Działanie

Tutaj jest niestety ciężej...
Mamy jakieś *znane* poprawne sekwencje w stylu:

- $\{1, 2, 5, 10, 20, 50\}$
- $\{c^{0}, c^{1}, c^{2}, c^{3}, \dots\}$
- $\{c_{1},c_{2},\dots,c_{n}\}$, gdzie $\forall_{i}c_{i} \text{ mod } c_{i+1} = 0$

> Jeżeli potrzebujemy sprawdzić coś niestandardowego, to najprawdopodobniej potrzebne będzie kryterium specyficzne do zadania.
