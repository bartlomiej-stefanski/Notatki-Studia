**Dane:**
$A_{1},\dots,A_{n}$ ciągi elementów z $\Sigma = \{0,1,\dots,k-1\}$.
Niech $l_{i}$ oznacza długość ciągu $A_{i}$, a $l_{\max} = \max(l_{i} : i=1\dots n)$.

> Rozmiarem danych nie jest $n$, tylko suma długości napisów.

**Zadanie:**
Uszeregować ciąg w kolejności leksykograficznej.

## Ciągi Tej Samej Długości – Radix Sort

Wykonamy tutaj $l = l_{\max}$ razy [[Alternatywne Sortowanie#Counting Sort|Sortowanie Przez Zliczanie]], na kolejno $l, l-1, \dots,1$-tych z kolei elementach napisu. Ważne jest, by sortowanie było *stabilne* – nie zmieniało kolejności elementów jeżeli nie musi.

Okazuje się, że to wystarczy.
Dowód okazuje się być bardzo prostą indukcją (od końca!).

> Intuicyjnie zaczynamy od przodu, bo początkowe elementy mają najważniejsze informacje – chcemy przejrzeć je na koniec, gdzie nie zostaną nadpisane.

### Złożoność Czasowa

Każdy element przeanalizujemy tylko raz w sortowaniu, więc algorytm działa liniowe względem ilości elementów we wszystkich napisach.

## Ciągi Różnej Długości

Oczywistym sposobem było by dopełnienie *krótszych* ciągów *najpierwszymi* elementami i zastosowanie Radix Sort, ale skutkować to będzie czasem działania $O((n + k)\cdot l_{\max})$.
Jeżeli ciągi są bardzo różnej długości, to algorytm ten okaże się bardzo nieefektywny!

### Lepszy Sposób

Naszym celem jest znalezienie algorytmu liniowego. Tym razem potrzebnych będzie *kilka kroków*.

#### 1

Utwórz listę $\text{niepuste}$ początkowo pustą :D.
Zachowajmy niezmiennik, że jest ona posortowana (na początku trywialne).

#### 2

Utwórzmy tablicę $\text{ciagi}[i] = \{A_{j} : l_{j} = i\}$, czyli przechowującą pod $i$ tym indeksem ciągi długości $i$.
Potrafimy to zrobić w czasie liniowym.

#### 3

Dla każdego $l$ z $\langle 1, l_{\max}\rangle$ kroków (zaczynając od $l_{\max}$) dodaj wszystkie elementy z $\text{ciagi}[l]$ do $\text{niepuste}$ przed wszystkie dotychczasowe elementy.
Posortuj stabilnie względem $l$-tego elementu.

#### Złożoność Obliczeniowa

Każdy element przejrzymy tylko raz podczas sortowania, więc znowu mamy czas liniowy.

### Poprawność

Dowód poprawności będzie się opierał na tym, że pomiędzy iteracjami zachowujemy niezmiennik: *elementy są posortowane leksykograficznie według fragmentu słów $l,\dots,l_{max}$*.

Kluczowym do dowiedzenia tego będzie stabilność sortowania oraz *faktycznie wykonanie sortowania*.