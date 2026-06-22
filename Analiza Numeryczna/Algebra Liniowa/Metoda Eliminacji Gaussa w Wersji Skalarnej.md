Niech będzie $A^{(1)}x = b^{(1)}$ takie, że $\det(A^{(1)}) \ne 0$, $A^{(1)} = [a_{i,j}^{(1)}]\in\mathbb{R}^{n\times n}$ oraz $b^{(1)} = [b_{1}^{(1)}, b_{2}^{(1)},\dots,b_{n}^{(1)}]^{T}$.

Wtedy będziemy standardowo przeprowadzać eliminację Gaussa wierszowo dla układu równań:
$$
\begin{align*}
\begin{cases}
a_{1,1}^{(1)}x_{1} + a_{1,2}^{(1)}x_{2} + a_{1,3}^{(1)}x_{3} + \dots + a_{1,n}^{(1)}x_{n}&= b_{1}^{(1)}\\
a_{2,1}^{(1)}x_{1} + a_{2,2}^{(1)}x_{2} + a_{2,3}^{(1)}x_{3} + \dots + a_{2,n}^{(1)}x_{n}&= b_{1}^{(1)}\\
\vdots\\
a_{n,1}^{(1)}x_{1} + a_{n,2}^{(1)}x_{2} + a_{n,3}^{(1)}x_{3} + \dots + a_{n,n}^{(1)}x_{n}&= b_{1}^{(1)}\\
\end{cases}
\end{align*}
$$
Załóżmy, że $a_{1,1}^{1} \ne 0$.
Dla $i = 2,3,\dots,n$  mnożymy pierwsze równanie przez $m_{i,1} = -\frac{a_{i,1}^{(1)}}{a_{1,1}^{1}}$ i dodajemy do i-tego równania. Otrzymamy równoważny układ:

> To wcale nie jest eliminacja $\tiny{g}$aussa

$$
\begin{align*}
\begin{cases}
a_{1,1}^{(2)}x_{1} + a_{1,2}^{(2)}x_{2} + a_{1,3}^{(2)}x_{3} + \dots + a_{1,n}^{(2)}x_{n}&= b_{1}^{(2)}\\
\ \ \ \ \ \ \ \ a_{2,2}^{(2)}x_{2} + a_{2,3}^{(2)}x_{3} + \dots + a_{2,n}^{(2)}x_{n}&= b_{1}^{(2)}\\
\ \ \ \ \ \ \ \ \vdots\\
\ \ \ \ \ \ \ \  a_{n,2}^{(2)}x_{2} + a_{n,3}^{(2)}x_{3} + \dots + a_{n,n}^{(2)}x_{n}&= b_{1}^{(2)}\\
\end{cases}
\end{align*}
$$
Gdzie:
$$
\begin{align*}
(i=2,3,\dots,n)\begin{cases}
a_{i,j}^{(2)} = a_{i,j}^{(1)} + m_{i,1}\\
b_{i}^{(2)} = b_{i}^{(1)} + m_{i,1}b_{1}^{(1)}
\end{cases}
\end{align*}
$$
Następnie jeśli $a_{2,2}^{(2)} \ne 0$, to eliminujemy z równań od $3$ do $n$ niewiadomą $x_{2}$.
Otrzymamy układ postaci $A^{(3)}x = b^{(3)}$
Po $n-1$ iteracjach otrzymamy układ postaci:
$$
\begin{align*}
\begin{cases}
a_{1,1}^{(n)}x_{1} + a_{1,2}^{(n)}x_{2} + a_{1,3}^{(n)}x_{3} + \dots + a_{1,n}^{(n)}x_{n}&= b_{1}^{(n)}\\
a_{2,2}^{(n)}x_{2} + a_{2,3}^{(n)}x_{3} + \dots + a_{2,n}^{(n)}x_{n}&= b_{1}^{(n)}\\
\vdots\\
 a_{n,n}^{(n)}x_{n}&= b_{1}^{(n)}\\
\end{cases}
\end{align*}
$$

#### Jawne Wzory na Współczynniki

Dla $r = 2,3,\dots,n$ oraz $i,j = r,r+1,\dots,n$:
$$
\begin{align*}
\begin{cases}
a_{i,j}^{(r)} &= a_{i,j}^{(j-1)} + m_{i,r-1}a_{r-1,j}^{(j-1)}\\
b_{i}^{(r)} &= b_{i}^{(r-1)} + m_{i},r-1b_{r-1}^{(r-1)}\\
m_{i,r-1} &= -\frac{a_{i,r-1}^{(r-1)}}{a_{r-1,r-1}^{(r-1)}}
\end{cases}
\end{align*}
$$
Współczynniki $a_{r,r}^{(r)}$ nazywamy elementami głównymi.

Dalej wystarczy rozwiązać układ trójkątny górny:
$$
x_{r} = (b_{r}^{(r)} - \sum\limits_{i=r+1}^{n}a_{r,j}^{n}x_{j})/a_{r,r}^{(r)}
$$
Rozwiązanie układu zajmie nam łącznie $O(n^{3})$.

> To jest *po prostu* eliminacja Gaussa, ale ładnie rozpisana.

## Metoda Eliminacji z Wyborem Elementów Głównych

Rozważmy sytuację, w której rozpisywany układ równań ma jednoznaczne rozwiązanie, *ale* dla pewnego $r, (1\le r \le n-1)$ jest $a_{i,i}^{1} \ne 0$ dla $i = 1,2,\dots,r-1$ oraz $a_{r,r}^{(r)} = 0$.
Nie możemy zatem wykonać kolejnego kroku.

Wystarczy jednak zamienić miejscami równania $r$-te i $p$-te, gdzie $p$ jest takie, że $r+1\le p \le n$ i  że $a_{p,r}^{(r)} \ne 0$.

**Uwaga (trudne do pokazania):**
Analiza błędów zaokrągleń ($\equiv \text{realizacja eliminacji Gaussa w arytmetyce fl}$) pokazuje, że warto postępować tak, aby wszystkie mnożniki $|m_{r,j}^{(r)}| < 1$.

Można to zrobić na dwa sposoby:

1. W $r$-tym kroku eliminacji Gaussa przestawiamy równania $r$-te i $p$-te gdzie $p\in\{r,\dots,n\}$ jest takie, że $|a_{p,r}^{(r-1)}| = \max_{r\le i \le n}|a_{i,r}^{(r)}|$.
   *Do domu:* Jak to zrobić, by całkowity czas nadal był $O(n^{3})$
2. Pełny wybór elementów głównych:
   W $r$-tym kroku eliminacji przestawiamy równania $r$-te i $p$-te, a także zamieniamy numerację niewiadomych $x_{r} \leftrightarrow x_{q}$, gdzie $p,q\in\{r,r+1,\dots,n\}$ są takie, że:
   $|a_{p,q}|^{(r)} = \max_{r\le i,j \le n}|a_{i,j}^{(r)}|$.

### Twierdzenie

Dla dowolnej macierzy $A\in\mathbb{R}^{n \times n}$ istnieją:

- macierz permutacji $P\in\mathbb{R}^{n\times n}$ (w każdym wierszu i każdej kolumnie dokładnie jedna jedynka i reszta zera)
- macierz $L = ◺\in\mathbb{R}^{n \times n}$
- macierz $L = ◹\in\mathbb{R}^{n \times n}$
