Takie podejście do rozwiązywania problemów jest poniekąd rozwinięciem podejścia [[Dziel i Zwyciężaj]].
Tutaj również głównym celem będzie redukcja problemu do mniejszych pod-problemów, ale podczas gdy częściowe pokrywanie się pod-problemów dla metody *dziel i zwyciężaj* skutkowało sporym spowolnieniem działania algorytmu tutaj uda się uniknąć tego problemu dzięki *jednorazowemu* rozpatrywaniu wspólnych problemów.

### Spamiętywanie

Takie podejście jest poniekąd gdzieś pomiędzy dziel i zwyciężaj. Zazwyczaj powstaje, gdy nasz algorytm algorytm działa wolno, zauważamy, że wielokrotnie rozważamy te same podproblemy, więc zaczynamy *cacheować* rozwiązania.

To pozwoli uniknąć ponownego rozpatrywania podproblemów, co faktycznie poprawi wydajność.
Często jednak nie będzie to *tak dobre rozwiązanie jak mogło by być* – musimy rekurencyjnie wchodzić do podproblemów i pytać się *"czy jest rozwiązany"* oraz często użyjemy więcej pamięci niż tak naprawdę potrzeba (być może nawet asymptotycznie więcej).

Z tego powodu zazwyczaj lepiej przejść do rozwiązania ze strategią programowania dynamicznego nawet jeżeli będzie ono nieco trudniejsze.

## Klasyczny Problem

![[Liczenie Dwumianu Newtona]]
