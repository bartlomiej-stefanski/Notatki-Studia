Niech $a \ne 0$, wtedy:
$$
\begin{align*}
ax + b= 0 &\implies x_{0} = -\frac{b}{a}\\
ax^{2}+bx+c=0 &\implies x_{1}=\dots, x_{2}=\dots\\
wiel\ 3,4 &\implies \text{jawny wzór}\\
wiel\ 5\dots &\implies \text{brak wzoru}\ \boxed {:(}
\end{align*}
$$
**Problem:** Niech dana będzie funkcja ciągła $f$. Znaleźć takie $\alpha$, że $f(\alpha) = 0$.
## Metoda Bisekcji

![[equation-solving-methon-bisection.png]]

Załóżmy, że funkcja $f$ jest ciągła w $[a_{0},b_{0}]$ i ma tam tylko jedno miejsce zerowe i ma tam tylko jedno miejsce zerowe $\alpha \in (a_{0},b_{0})$ i że $f(a) \cdot f(b) < 0$.

Skonstruujmy ciąg przedziałów:
$$
\begin{align*}
I_{k} = [a_{k},b_{k}] \tag{k = 0,1,...}
\end{align*}
$$
O własności:
$$
I_{0} > I_{1} > I_{2} > \dots > I_{k} > \dots\ \ \ \text{oraz}\ \ \ \forall_k\alpha \in I_{k}
$$
Wtedy dla każdego przedziału, by wyznaczyć następny:

1. Policzmy środek przedziału $I_{k}$: $m_{k+1} = \frac{a_{k}+b_{k}}{2}$
2. Jeżeli $f(m_{k+1}) = 0 \implies STOP \land \alpha = m_{k+1}$

No i teraz *formalna* definicja funkcji:
$$
\begin{align*}
I_{k+1} = [a_{k+1},b_{k+1}] = \begin{cases}
[m_{k+1},b_{k}]&:f(m_{k+1})f(b_{k}) < 0\\
[a_{k},m_{k+1}]&:f(m_{k+1})f(b_{k}) > 0
\end{cases}
\end{align*}
$$
### Obserwacje

- W wyniku metody bijekcji otrzymujemy przedział o długości:
$$
\frac{b_{0}-a_{0}}{2^{n}} \overset{n\rightarrow\infty}{\rightarrow} 0 \implies lim_{n\rightarrow\infty}m_{n+1} = \alpha
$$
- Zbieżność metody bisekcji jest wolna (1 cyfra dwójkowa na iterację)
- Zbieżność metody nie zależy od rozpatrywanej funkcji
- Algorytm wyznaczania przedziału zawierającego $\alpha$ o długości $\epsilon$ wymaga
  $\lfloor log_{2}\frac{b_{n}-a_{n}}{2\cdot\epsilon} \rfloor + 1$ kroków

## Metoda Newtona

![[equation-solving-newtons-method.png]]

Dla danego $x_{0}$:
$$
\begin{align*}
x_{n+1} &= x_{n} - \frac{f(x_{n})}{f'(x_{n})} \tag{n=0,1,2,3,...}\\
y &= f'(x_{0})(x - x_{0}) + f(x_{0})\\
x_{n} &: \text{miejsce zerowe } f(x)\\
&\Downarrow\\
0 &= f'(x_{0})(x-x_{0}) + f(x_{0})
\end{align*}
$$

**Problem:** Co jeśli nie znamy jawnego wzoru na pochodną?

## Metoda Siecznych

![[equation-solving-scant-method.png]]

Dla danego $x_{0}, x_{1}$:
$$
\begin{align*}
x_{n+1} &= x_{n} - \frac{f(x_{n})}{\frac{f(x_{n}) - f(x_{n-1})}{x_{n}-x_{-1}}} \tag{n=1,2,...}
\end{align*}
$$

Warto zauważyć, że mianownik ułamka przybliża pochodną – robimy prawie to samo co dla metody Newtona.

## Uwagi i Różności

### Warunek Stopu

Dla metody iteracyjnej warunek stopu definiujemy następująco:
$$
\begin{align*}
&|f(x_{1})| < \delta_{mała}\\
\text{lub}&\\
&\left| \frac{x_{n+1} - x_{n}}{x_{n}} \right|, \left| \frac{x_{n+2} - x_{n+1}}{x_{n+1}} \right|,\dots,\left| \frac{x_{n+m} - x_{n+m-1}}{x_{n+m-1}} \right| < \epsilon_{małe}\\
\text{lub}&\\
&n \ge N_{max}
\end{align*}
$$
Pozwoli to uniknąć nieprzyjemnych przypadków, gdzie np. funkcja na całym przedziale jest mniejsza od $\delta$.
