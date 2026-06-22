---

---
> Skrótowo NIFS3

Dla zestawu punktów $x_k$ będziemy chcieli mieć taką funkcję, że:

- $S(x_{k}) = y_{k}$ – w wybranych punktach jest równa funkcji
- dla $x \in [x_{k-1}, x_{k}]$, $S\in\prod_{3}$
- $S, S', S''$ – funkcje ciągłe na $[x_{0}, x_{n}]$

Oraz dodatkowy warunek, by funkcja była *naturalna*:

- $S''(x_{0}) = S''(x_{n}) = 0$

> Dla innych *typów* funkcji sklejanej *warunki dodatkowe* będą inne, ale zawsze dwa.
> Np. dla *cyklicznej funkcji* sklejanej będzie $S'(x_{0}) = S'(x_{n}) \land S''(x_{0}) = S''(x_{n})$.

Te warunki są po to, by funkcja na przedziale układała się *ładnie* i wyglądała *naturalnie*.

### Przykład

Znajdźmy NIFS3 dla danych:
$$
\begin{array}{c|c c c}
x_{k} & -1 & 0 & 1 \\
\hline
y_{k} & 1 & -1 & 1
\end{array}
$$
Stąd otrzymamy układ równań:
$$
\begin{align*}
S(x) = \begin{cases}
Ax^{3} + bx^{2} + Cx + D\\
Ex^{3} + Fx^{2} + Gx + H
\end{cases}
\end{align*}
$$
Szukamy $A, B, C, D, E, F, G, H$.

Ciągłość i interpolacja:
$$
\begin{align*}
&\begin{cases}
S_{1}(-1) = 1\\
S_{1}(0) = S_{2}(x) = -1\\
S_{2}(1) = 1
\end{cases}
\implies
\begin{cases}
-A + B -C + D = 1\\
D = H = -1\\
E + F + G + H = 1
\end{cases}
\end{align*}
$$
Ciągłość pochodnych:
$$
\begin{align*}
&S'(x) = \begin{cases}
3Ax^{2} + 2Bx + C : [-1,0]\\
3Ex^{2} + 2Fx + G : [0,1]
\end{cases}\\
&S''(x) =\begin{cases}
6Ax + 2B : [-1,0]\\
6Ex + 2F : [0,1]
\end{cases}
\end{align*}
$$
By Były ciągłe musi zachodzić: $S'_{1}(0) = S'_{2}(0)$ oraz $S''_{1}(0) = S''_{2}(0)$.
By były *naturalne* musi zachodzić: $S''_{1}(-1) = S''_{2}(1) = 0$.

Otrzymujemy z tego równanie:
$$
C=G, 2B=2F, -6A+2B = 0, 6E+2F = 0
$$
Więc mamy już rozwiązanie patrząc jeszcze na poprzednie równania:
$$
\begin{align*}
\begin{cases}
A = 1\\
B = 3\\
C = 0\\
D = -1
\end{cases}
\begin{cases}
E = -1\\
F = 3\\
G = 0\\
H = -1
\end{cases}
\implies S(x) = \begin{cases}
x^{3}+3x^{2}-1 : x\in[-1,0]\\
-x^{3}+3x^{2}-1 : x\in[0,1]
\end{cases}
\end{align*}
$$

Tada!
Ciekawe, czy istnieje jakieś narzędzie, które zrobi to za nas...

### W Jaki Sposób Efektywnie Konstruować NIFS3?

Nawet wtedy gdy węzłów będzie *dużo*?
Oczywiście metoda pokazana w przykładzie jest zbyt wolna...

#### Twierdzenie

Dla danych $x_{0} < x_{1} < \dots < x_{n}$ oraz $y_{0},y_{1},\dots,y_{n} \in \mathbb{R}$ zawsze istnieje *dokładnie jedna* NIFS3 spełniająca warunki.

1. $S(x_{k}) = y_{k}$ dla każdego $k \in \{0, \dots, n\}$
2. $S |_{[x_{k-1}, x_{k}]} \in \prod_{3}$
3. $S,S',S'' \in C[x_{0},x_{n}]$
4. $S''(x_{0}) = S''(x_{n}) = 0$

Dla tego $S$ istnieje jawny wzór w każdym $[x_{k-1}, x_{k}]$ dla $k\in \{1,\dots,n\}$:
$$
\begin{align*}
s(x) &= h_{k}^{-1}\left[
\frac{1}{6}M_{k-1}(x_{k}-x)^{3} +
\frac{1}{6}M_{k}(x-x_{k-1})^{3} +
\left(f(x_{k-1}) - \frac{1}{6}M_{k-1}h_{k}^{2}\right)(x_{k}-x) +
\left(f(x_{k}) - \frac{1}{6}M_{k}h_{k}^{2}\right)(x-x_{k-1})
\right]
\end{align*}
$$

Wzór ten zależy od tak zwanych *momentów*, czyli wielkości postaci:
$$
\begin{align*}
M_{k} = S''(x_{k})\tag{k = 0, 1, ..., n}
\end{align*}
$$
Momenty $M_{k}$ spełniają układ równań postaci:
$$
\begin{align*}
\lambda_{k}M_{k-1} + 2M_{k} + (1-\lambda_{k})M_{k+1} &= d_{k}\tag{k = 1, ..., n-1}\\
\lambda_{k} &= \frac{h_{k}}{h_{k} + h_{k+1}}\\
h_{k} &= x_{k} - x_{k-1}
\end{align*}
$$
Jest to układ równań liniowych.
Zapiszmy go w postaci macierzy:
$$
\begin{align*}
\begin{bmatrix}
2 & 1 - \lambda_{1} &   \\
\lambda_{2} & 2 & 1 - \lambda_{2} & \\
 & \lambda_{3} & 2 & 1 - \lambda_{3}\\
&  & \ddots & \ddots & \ddots\\
& & & \ddots & \ddots & \ddots\\
& & & & \lambda_{n-2} & 2 & 1 - \lambda_{n-2}\\
& & & & & \lambda_{n-1} & 2
\end{bmatrix}
\begin{bmatrix}
M_{1} \\ M_{2} \\ M_{3} \\ \vdots \\ \vdots \\M_{n-2} \\ M_{n-1}
\end{bmatrix}
&= 
\begin{bmatrix}
d_{1} \\ d_{2} \\ d_{3} \\ \vdots \\ \vdots \\ d_{n-2} \\ d_{n-1}
\end{bmatrix}
\end{align*}
$$
**Obserwacja:** Powyższy układ równań można rozwiązać w czasie $O(n)$ – to na ćwiczeniach.

> Do tego używa się algorytmu Tomasa

#### Wniosek

NIFS3 dla danych $n+1$ węzłów może być skonstruowana w czasie $O(n)$ – liniowo względem liczby węzłów.

## Podrabianie Podpisów – Krzywe Parametryczne

Krzywa Parametryczna:
$$
\begin{align*}
\gamma(t) &= [(x(t), y(t))\in\mathbb{R}^{2} : a \le t \le b]
\end{align*}
$$
- $x(t)$ – ruch po osi OX
- $y(t)$ – ruch po osi OY

### Przykład – Kółko

$$
\gamma(t) = [(a\cdot \cos(t), a \cdot \sin(t)) : 0 \le t \le 2\pi]
$$
![[circle-curve.png]]

Jest to tak naprawdę zbiór punktów do interpolacji:
$$
\begin{array}{c|c|c}
x_{0} & x_{1} & x_{2} & x_{3} & \dots & x_{n} \\
\hline
y_{0} & y_{1} & y_{2} & y_{3} & \dots & y_{n}
\end{array}
$$
Stąd możemy otrzymać tabelki zależne od *czasu*:
$$
S_{x}(t) = \begin{array}{c c c c}
t_{0} & t_{1} & t_{2} & t_{3} & \dots & t_{n} \\
\hline
x_{0} & x_{1} & x_{2} & x_{3} & \dots & x_{n}
\end{array}\ \ \ \ \ \ 
S_{y}(t) = \begin{array}{c c c c}
t_{0} & t_{1} & t_{2} & t_{3} & \dots & t{n} \\
\hline
y_{0} & y_{1} & y_{2} & y_{3} & \dots & y_{n}
\end{array}
$$
Obie funkcje $S$ możemy wyznaczyć korzystając z NIFS-3.
Z tego wyciągamy krzywą parametryczną:
$$
\gamma(t) = [(S_{x}(t), S_{y}(t)) : t_{0} \le t \le t_{n}]
$$
