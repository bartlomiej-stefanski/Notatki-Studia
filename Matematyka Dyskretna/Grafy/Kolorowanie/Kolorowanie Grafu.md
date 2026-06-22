---
tags:
  - MDM-checklist
---
Dla grafów $G$ bez pętli.
Kolorowanie polega na przyporządkowaniu kolorów wierzchołkom w taki sposób, że żadnych dwóch sąsiadów nie ma takiego samego koloru.

- Graf $G$ jest **$k$-kolorowalny** jeśli można go pokolorować $k$ kolorami.
- **Liczba Chromatyczna** $\chi(G)$ oznacza minimalne $k$, takie, że graf jest k-kolorowalny

## Fakty

- $\chi(G) = 1\iff$ graf jest pusty ($|E| = 0$)
- $\chi(G) = 2\iff$ graf jest dwudzielny
- $\chi(G) \ge 3$ – nie wiadomo (problem np-zupełny)
- $H\subseteq G \implies \chi(H) \le \chi(G)$
- $K_{k}\subseteq G \implies \chi(G) \ge k$

- W każdym kolorowaniu podzbiór jednego koloru jest niezależny.
- Jeśli $k$ jest rozmiarem największego podzbioru niezależnego w $G$ to $\chi(G) \ge \frac{n}{k}$
	- Dowód przez szufladki
- Tw. Brooksa: $\chi(G) = \deg(G) + 1 \iff G$ jest kliką lub cyklem długości nieparzystej
- $\chi(G) + \chi(\widetilde{G}) \le n+1$
- $\chi(G) \le \deg(G) + 1$

