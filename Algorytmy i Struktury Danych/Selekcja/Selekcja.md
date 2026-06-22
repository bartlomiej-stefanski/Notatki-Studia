**Dane:**
Ciąg elementów $T[1\dots n]$ z porządkiem liniowym.

> Zakładamy bez straty ogólności, że liczby są różne.

**Zadanie:**
Znaleźć $k$-tą liczbę w kolejności według danego porządku – wartość znana podczas tworzenia algorytmu.

## Szczególne Przypadki

### K = 1

Dosyć *oczywiste*, że wystarczy $n-1$ porównań.

### K = 2

[[AISD Lista 5#Zadanie 8|Można Pokazać]], że istnieje taki algorytm, który potrzebuje co najwyżej $n -2 + \lfloor \log_{2} n \rfloor$ porównań.

Opiera się on na obserwacji, że wyznaczając element drugi-największy wyznaczymy przy okazji element największy – problem dla `k=2` zawiera w sobie problem `k=1`.
Teraz pytaniem jest jak najlepiej można wykorzystać informacje z problemu `k=1`?

Okazuje się, że wystarczy sprawdzić elementy, które przegrały z elementem największym – tylko ta grupa elementów może zawierać drugi największy, a nie mamy więcej informacji, by lepiej ograniczyć zbiór możliwych elementów.
