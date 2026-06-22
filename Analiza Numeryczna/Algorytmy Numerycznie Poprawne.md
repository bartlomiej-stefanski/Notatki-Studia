## Definicja

Algorytm nazywamy numerycznie poprawnym, jeśli wynik jego działania w arytmetyce *fl* może zostać zinterpretowany jako *mało zaburzony wynik dokładny* dla *mało zaburzonych danych*.

**Mało** – skończenie bardzo.

## Przykład – wartość funkcji dwóch zmiennych

Chcemy obliczyć wartość funkcji dwóch zmiennych $A(a,b)$.  
Niech $Alg_{A}(a,b)$ oznacza algorytm obliczania wartości $A(a,b)$.

- Wynik dokładny dla mało zaburzonych danych:
  $fl(Alg_{A}(a,b)) = A(a(1+\alpha),b(1+\beta))$
- Mało zaburzony wynik dla mało zaburzonych danych:
  $fl(Alg_{A}(a,b)) = A(a(1+\alpha),b(1+\beta))(1+\gamma)$

$|\gamma|,|\alpha|,|\beta| \le k \cdot 2^{-t}$

**Wnioski:** 

1. Algorytm numerycznie poprawny **i** zadanie dobrze uwarunkowane $\implies$ sukces
2. Algorytm numerycznie poprawny **i** zadanie źle uwarunkowane $\implies$ prawie zawsze źle

## Przykład

Niech dany będzie algorytm następujący algorytm wyliczający sumę $x_{1},\dots,x_{n}$:
```
s := x[1]
for i = 2 to n
    s = s + x[n]

return s
```

$$
\begin{align*}
fl(S) &= (\dots(((x_{1} + x_{2})(1 + \epsilon_{2}) +x_{3})(1+\epsilon_{3}) + x_{4})(1 + \epsilon_{4}) + \dots + x_{n})(1+\epsilon_{n}) \\
&= \boxed{zadanie\ domowe} \\
(\text{dla } |\epsilon_{i}|\le2^{-t}) &= \sum\limits_{i=1}^{n}{x_{i}\prod_{j=i}^{n}(1 + \epsilon_{j})}\\
\text{(Tw. o kumulacji błędów)}&= \sum\limits_{i=1}^{n}x_{i}(1+E_{i}) \\
&= \sum\limits_{i=1}^{n}{\widetilde{x}_{i}}
\end{align*}
$$

Jest to wynik dokładny $\left(\sum\right)$ dla mało zniekształconych danych $(\widetilde{x}_{i})$

**Ważne:**

- Nie wolno szacować przy sprawdzaniu – tylko przejścia równoważne
- W każdym miejscu należy przyjąć taki sam błąd dla danej zmiennej
