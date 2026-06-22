Algorytm znajdujący [[Drzewo Spinające#Minimalne Drzewo Spinające|Minimalne Drzewo Spinające]].

## Strategia

Zaczynamy od $V' = \{v\}$ – losowo wybrany wierzchołek oraz $E'$ składającego się z krawędzi wychodzących z $v$.

W każdym kroku wybieramy najtańszą krawędź z $E'$ prowadzącą do wierzchołka $u\not\in V'$ i dodajemy ją do rozwiązania. Dopisujemy $u$ do $V'$ oraz krawędzie wychodzące z $u$ do $E'$.
Kończymy, gdy $V' = V$.

> Wygodnie implementuje się używając [[Kolejka Priorytetowa|kolejki priorytetowej]].

## Dowód Poprawności

> Właściwie to szkic, no ale no...

Indukcyjnie pokazujemy niezmiennik dla coraz większych zbiorów: wybrane krawędzie **są** krawędziami MST zbudowanego dla przetwarzanego podzbioru wierzchołków.
To oczywiście prowadzi do wniosku, że uzyskamy MST dla wszystkich wierzchołków.

Dodanie nowego wierzchołka w kroku indukcyjnym można argumentować z tego, że wybieramy najtańszą krawędź która łączy aktualną SSS z inną (no a jakaś musi istnieć).
