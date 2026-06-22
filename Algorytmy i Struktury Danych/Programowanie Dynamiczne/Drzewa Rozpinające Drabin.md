#### Definicja Drabin

Drabiną $D_{7}$ nazywamy graf z rysunku poniżej:
![[Drzewo-drabin.svg]]
Konstrukcja uogólnia się na $D_{n}$.

#### Problem

**Dane:**

- Liczby naturalne $n,k$
- Ciąg par liczb naturalnych $(u_{i},v_{i})$ dla $i = 1,\dots,m$
	- Są to wyróżnione krawędzie w $n$-elementowej drabinie

**Zadanie:**
Liczba drzew rozpinających o $k$ krawędziach wyróżnionych.

## Analiza Problemu

> Przez $D_{i}$ oznaczana będzie $i$-elementowa pod-drabina $D_{n}$.

Najpierw rozważymy prostszy problem wyznaczania liczb rozpinających drabiny $D_{i}$ bez uwzględnienia krawędzi wyróżnionych.

**Fakt 1:**
Dla drzewa rozpinającego $T$ drabinę $D_{i+1}$ mamy $T \cap D_{i}$ będące:

- Drzewem rozpinającym drabinę $D_{i}$
- lasem rozpinającym $D_{i}$ złożonym z dwóch drzew – jedno zawiera wierzchołek $i$, a drugie $i'$.

Teraz dla każdego $D_{i}$ będziemy chcieli wyznaczać $S_{i}$ oraz $N_{i}$ – odpowiednio zbiór drzew spinających oraz dwu-elementowych lasów spinających drabinę $D_{i}$ takich, że $i,i'$ są w innych lasach.

Zauważamy, że na podstawie wcześniejszych $S_{i},N_{i}$ potrafimy generować następne:
**Fakt 2:**
$$
\begin{align*}
|S_{1}| &= |N_{1}| = 1 && (1)\\
 \\
|S_{i}| &= 3|S_{i-1}| + |N_{i-1}| &&(2)\\
|N_{i}| &= 2|S_{i-1}| + |N_{i-1}| && (3)
\end{align*}
$$
1. Oczywiste
2. Dla $S_{i-1}$ mamy do dodania dwie z trzech krawędzi $\{(i-1)\leadsto i, i\leadsto i', (i-1)'\leadsto i'\}$, więc łącznie trzy możliwości. Dla $N_{i-1}$ możemy jedynie dodać $(i-1)\leadsto i$ i $(i-1)'\leadsto i'$.
3. Przechodząc z $S_{i-1}$ możemy dodać rozłącznie krawędź$(i-1)\leadsto i$ lub $(i-1)'\leadsto i'$.
   Dla $N_{i-1}$ możemy jedynie dodać $(i-1)\leadsto i$ i $(i-1)'\leadsto i'$.

### Rozwiązanie

Wykorzystamy konstrukcję z $S_{i},N_{i}$, ale do każdego zbioru dodamy parametr zliczający *'zawarte wyróżnione krawędzie'*.
Wtedy przechodząc do $S_{i+1},N_{i+1}$ uaktualnimy wartości odpowiadające wybranej liczbie wyróżnionych krawędzi w tym kroku.
