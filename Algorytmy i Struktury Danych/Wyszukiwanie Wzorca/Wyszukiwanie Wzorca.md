**Dane:**

- $T = \langle t_{1},t_{2},\dots,t_{n}\rangle$ – text
- $P = \langle p_{1},p_{2},\dots,p_{m}\rangle$ – wzorzec

**Zadanie:**
Znaleźć wszystkie wystąpienia wzorca.
Formalnie wszystkie takie $i$, że $\forall_{j\in\{i, i+1, \dots, i+m-1\}}t_{j} = p_{j}$.

> Algorytm naiwny dla każdego możliwego początku $t_{i}$ próbuje dopasować od tej pozycji wzorzec

Lepiej można to zrobić:

- Algorytmem [[Karp Rabin|Karpa Rabina]]
- [[Wyszukiwanie Automatem Skończonym|Automatem Skończonym]]
- Algorytmem [[KMP]]
	- (nie obowiązkowe) Lub [[MKMP]] jeżeli potrzebujemy wyszukiwać wielu wzorców
