Efektywność (złożoność?) algorytmów będziemy określać jako funkcję rozmiarów danych.  
Posłużą nam do tego następujące symbole:
![[Symbole Asymptotyczne]]

- *Złożoność czasowa* – liczba jednostek czasu potrzebna na wykonanie algorytmu.
- *Złożoność pamięciowa* – liczba jednostek pamięci (np. komórek, bitów) potrzebnych na wykonanie algorytmu.

Obie złożoności możemy wyznaczać w dwóch *wariantach*:

- *Złożoność najgorszego przypadku (pesymistyczna)* – maksymalny koszt obliczeń dla danych określonego rozmiaru.
- *Złożoność średniego przypadku (oczekiwana)* – wyznaczamy tak jak [[Wartość Oczekiwana|wartość oczekiwaną]]: $\sum\limits_{d\in\text{dane}} \text{koszt}(d) \cdot P(d)$

### Jednostka Czasu
#### Kryterium Jednorodne

Każda podstawowa instrukcja (np. maszyny RAM) zajmuje czas jednostkowy – liczymy ile operacji maszyny ram wymaga wykonanie algorytmu.

#### Kryterium Logarytmiczne

Koszt każdej podstawowej instrukcji maszyny wymaga czasu proporcjonalnego do długości zmiennych na których operujemy.

Być może lepiej odwzorowuje rzeczywistość, ale będziemy używać tego kryterium tylko gdy przerabiane dane były by *naprawdę duże*.
