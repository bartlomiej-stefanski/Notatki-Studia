
![[Postaci Wielomianów#Postać Lagrange'a]]

### Przybliżenie

Dla danych pomiarów różnych  $x_{0}, x_{1}, \dots, x_{n}\ \ (i \ne j \implies x_{i}\ne x_{j})$ liczb rzeczywistych, oraz opowiadających im wartości $y_{0}, y_{1}, \dots, y_{n}$ będziemy potrafili znaleźć taki wielomian $L_{n}$, dla którego: 
- $L_{n} \in \prod_{n}$ 
- $L_{n}(x_{k}) = y_{k}\ \ \ \ (0 \le k \le n)$

#### Obserwacje

- $\lambda_{k} \in \prod_{k} \setminus \prod_{k-1}$
- $\lambda_{k}(x_{j}) =$
    - $1 : (k = j)$
    - $0 : (k \ne j)$

Stąd $L(x_{k}) = y_{k}$

### Twierdzenie o Istnieniu Interpolacji Lagrange'a

Zadanie interpolacji wielomianowej Lagrange'a ma *zawsze* jednoznaczne rozwiązanie.

> Jako zadanie domowe, które *może* gdzieś się kiedyś pojawi...

To można pokazać zakładając nie-wprost, że istnieją dwa wielomiany $N$-tego stopnia interpolujące $N$ punktów.
Po odjęciu tych wielomianów dostalibyśmy $N+1$ miejsc zerowych.

### Przykład 1

$f(x) = e^{x}, n = 3, x_{0} = 0, x_{1} = 0.2, x_{2} = 0.6, x_{3} = 0.8$.

Użyjmy interpolacji wielomianu do przybliżenia $f(0.4)$, ale jedynie na podstawie informacji $(x_{i},f(x_{i})), i \in \{0,1,2,3\}$.
$$
\begin{array}{c|c c}
 y_{k} & 0 & 0.2 & 0.6 & 0.8\\
\hline
y_{k} & 1 & 1.22\dots & 1.82 & 2.22\dots
\end{array}
$$

$$
\begin{align*}
L_{3} &= y_{0}\lambda_{0}(x) + y_{1}\lambda_{1}(x) + y_{2}\lambda_{2}(x) + y_{3}\lambda_{3}(x)\\
\lambda_{0}(x) &= \frac{(x-x_{1})(x-x_{2})(x-x_{3})}{(x_{0}-x_{1})(x_{0}-x_{2})(x_{0}-x_{3})} = -\frac{1}{0.096}(x-0.2)(x-0.6)(x-0.8)\\
\dots\\
1.4918\dots &= f(0.4) \approx L_{3}(0.4) = 1.4914\dots
\end{align*}
$$

### Przykład 2

Niech $f(x) = x^{6}$. Weźmy parami różne węzły $x_{0},x_{1},\dots,x_{2024}$.
Wtedy $L_{2024}(x) = x^{6}$, bo istnieje tylko jeden taki wielomian.

Praktycznie jednak obliczane wartości $L_{2024}$ będą wyraźnie różne od $f$ przez utratę precyzji w arytmetyce modulo.
