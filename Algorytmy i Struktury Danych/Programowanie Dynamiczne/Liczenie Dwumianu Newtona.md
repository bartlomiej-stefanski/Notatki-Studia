**Zadanie:**
Policzyć $\binom{n}{k}$.

## Podejście Dziel i Zwyciężaj

Zachodzi wzór $\binom{n}{k} = \binom{n}{k-1} + \binom{n-1}{k-1}$.
Możemy więc wywoływać się rekurencyjnie i kończyć, gdy $n=0$ lub $n=k$.

#### Problem

Powstanie bardzo dużo mniejszych problemów do rozwiązania – każde dzielenie skończymy dopiero, dla $\binom{n'}{k'} = 1$. Musimy więc dotrzeć $\binom{n}{k}$ razy do jedynki, więc mamy bardzo słabą złożoność obliczeniową.

**Obserwacja:**
Wielokrotnie rozwiążemy problem dla danych $n,k$.

### Spamiętywanie

Możemy pamiętać każde obliczone $\binom{n}{k}$ i od razu zwracać wynik przy zapytaniu o wartość.
Ale *ładniej*, szybciej i oszczędniej pamięciowo będzie skorzystać z programowania dynamicznego.

## Programowanie Dynamiczne

Zaczniemy wyliczanie wartości *sekwencyjnie* – od najmniejszych wartości 

