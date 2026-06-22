W typowym schemacie dowodu będziemy mieli *adwersarza* oraz *algorytm*.
*Algorytm* rozwiązuje problem zadając pytania adwersarzowi dotyczące danych dla problemu, a *adwersarz* odpowiada na pytania, tak by odpowiedzi były spójne oraz by algorytm wykonał maksymalnie wiele pytań.
W szczególności *adwersarz* nie ustala zestawu danych. Musi jedynie odpowiadać na pytania tak, by istniał zestaw danych, dla którego odpowiedzi będą zgodne.

Najlepiej jednak chyba na przykładzie...

## Przykład

### MinMax

Pokażemy, że algorytm [[MinMax]] musi wykonać co najmniej $\left\lceil  \frac{3}{2} n -2 \right\rceil$ porównań. W tym celu rozważymy grę pomiędzy algorytmem, a złośliwym adwersarzem.

- Cel *algorytmu*: wskazanie indeksów minimalnego i maksymalnego elementu zbioru $S$ wykonując minimalnie wiele porównań.
- Cel *adwersarza*: zmuszenie algorytmu do wykonania co najmniej $\left\lceil  \frac{3}{2}n - 2  \right\rceil$ pytań

Koniec gry nastąpi, gdy *algorytm* będzie pewien wyznaczonych indeksów.

> Tezę pokażemy jeśli niezależnie od algorytmu adwersarz zawsze będzie w stanie wymusić zadanie $\left\lceil  \frac{3}{2}n - 2  \right\rceil$ pytań.

#### Strategia Adwersarza

Będzie na czas gry utrzymywał cztery zbiory $A,B,C,D$ w taki sposób, by:

- $A = \{i \mid a_{i} \text{ jeszcze nie był porównywany}\}$
- $B = \{i \mid a_{i} \text{ wygrał jakieś porównanie i nie przegrał rzadnego}\}$
- $C = \{i \mid a_{i} \text{ przegrał jakieś porównanie i nie wygrał rzadnego} \}$
- $D = \{i \mid a_{i} \text{ wygrał i przegrał jakieś porównanie}\}$

> Na początku oczywiście $|A| = n, B=C=D = \emptyset$

Następnie wykonujemy obserwacje dotyczące tego w jaki sposób pytania algorytmu mogą wpływać na przemieszczanie się elementów pomiędzy zbiorami:

- Jedno zapytanie może usunąć co najwyżej dwa elementy z $A$
- Porównanie w którym uczestniczy element z $A$ może nie zwiększać liczby elementów $D$
	- Jeżeli porównujemy np. $a\in A,b\in B$, to wybieramy, że $b$ wygrywa co nie zmienia $D$
- Dodanie jednego elementu do $D$ może wymagać jednego porównania:
	- Dla każdego porównania oprócz takich, gdzie bierzemy dwa elementy z $B$ lub $C$ istnieje wynik, który nie przesuwa żadnego elementu do $D$

**Fakt:**
Dopóki w zbiorze $A$ jest co najmniej jeden element lub zbiory $B,C$ nie są singletonami, to *algorytm* nie może jednoznacznie wskazać odpowiedzi.
To jest raczej oczywiste.

##### Odpowiedzi Adwersarza

Na pytania będzie udzielać odpowiedzi tak, by o ile to możliwe, żadne elementy nie trafiały do zbioru $D$.

##### Strategia Jest Wygrywająca

Na mocy wcześniejszych obserwacji, by opróżnić zbiór $A$ potrzeba co najmniej $\left\lceil  \frac{n}{2}  \right\rceil$ operacji przy czym żadna z nich nie doda elementu do zbioru $D$.
Dalej, by przenieść $n-2$ elementy do zbioru $D$ potrzebujemy wykonać $n-2$ porównania (znowu wcześniejsze obserwacje).
To daje nam łącznie $\left\lceil  \frac{3}{2}n -2 \right\rceil$ operacji do wykonania.