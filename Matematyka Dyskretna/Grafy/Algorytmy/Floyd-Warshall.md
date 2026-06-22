---
tags:
  - MDM-checklist
---
**Dane:**
Graf $G(V,E)$.
Funkcja wagowa $c: E \to R$ (zakładamy, że nie istnieją ujemne cykle).

**Zadanie:**
Wyznaczyć odległości pomiędzy wszystkimi parami wierzchołków.

## Algorytm

Kluczową obserwacją jest to, że znowu problem znajdowania ścieżki możemy podzielić na pod-problemy – zamiast szukać kosztu ścieżki $i\leadsto j$ można poszukać kosztów $i \leadsto k$ i $k\leadsto j$, co będzie prostsze (być może). Skąd wiemy jakie $k$ wybrać? Nie wiemy, więc sprawdzamy wszystkie:
$$
\begin{align*}
dp[i][j] = \begin{cases}
0 &: i = j \\
c(\{i,j\}) &: \{i,j\} \in E \\
\min_{k\in V\setminus\{i, j\}}(dp[i][k] + dp[k][j]) &: \text{w p.p.}
\end{cases}
\end{align*}
$$

Poniżej możliwa implementacja (oczekiwane jest, że początkowo tablica odpowiada macierzy sąsiedztwa):
```pascal
for k = 1 to n do
	for i = 1 to n do
		for j = 1 to n do
			if c[i,j] > c[i,k] + c[k,j]
				then c[i,j] := c[i,k] + c[k,j]
```

Złożoność obliczeniowa oczywiście $O(n^{3})$.

## Znajdywanie Przechodniego Domknięcia

Dla grafu $G$ chcemy wyznaczyć graf $G*$ taki, że jeśli w $G$ istnieje ścieżka z $v$ do $u$, to w $G*$ jest krawędź $v,u$.

Do rozwiązania tego problemu używa się zmodyfikowanego algorytmu Warshall'a:
```pascal
for k = 1 to n do
	for i = 1 to n do
		for j = 1 to n do
			// Nowa krawędź jeśli była w G
			// lub istnieje pośrednia ścieżka przez k
			c[i,j] := c[i,j] OR (c[i,k] AND c[k,j])
```
