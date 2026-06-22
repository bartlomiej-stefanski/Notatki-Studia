> Szczególny przypadek [[Kwadratura Liniowa|Kwadratury Liniowej]].

![[Postaci Wielomianów#Postać Lagrange'a]]

Niech dana będzie funkcja (ciągła) $f$ oraz parami różne węzły $x_{0}^{(n)}, x_{1}^{(n)},\dots$, a wtedy możemy łatwo wyznaczyć postać Lagrange'a.

Scałkujmy wielomian interpolacyjny $L_{n}$ w ustalonym przedziale $[a,b]$:
$$
\begin{align*}
\int\limits_{a}^{b}L_{n}(x)dx &= \sum\limits_{k=0}^{n}\left(\int\limits_{a}^{b}\left(\prod_{i=0,i\ne k}^{n}\frac{x-x_{i}^{(n)}}{x_{k}^{(n)}-x_{i}^{(n)}}\right)dx\right)f\left(x_{k}^{(n)}\right) = Q_{n}(f)\\
\\
\text{Gdzie}:&\\
&\begin{cases}
Q_{n}(f) = \sum\limits_{k=0}^{n}A_{k}^{(n)}f(x)\\
A_{k}^{(n)} = \int\limits_{a}^{b}\left(\prod\limits_{i=0,i\ne k}^{n}\frac{x-x_{i}^{(n)}}{x_{k}^{(n)}-x_{i}^{(n)}}\right)dx
\end{cases}
\end{align*}
$$
**Problem:**
Policzenie współczynników wymaga policzenia całki...

> Da się to zrobić w czasie $O(n^{2})$

### Błąd Kwadratury Interpolacyjnej

![[Błąd Interpolacji#Twierdzenie]]

By poznać wartość błędu przybliżenia całki wystarczy scałkować wzór na błąd interpolacji:
$$
\begin{align*}
R_{n}(f) &= \frac{1}{(n+1)!}\int\limits_{a}^{b}f^{(n+1)}(\xi_{x})\cdot(x-x_{0}^{(n)})(x-x_{1}^{(n)})\dots(x-x_{n}^{(n)})dx
\end{align*}
$$
### Przykład

- $[a,b] = [0,1]$
- $n=4$
- $\{x_{0}^{(4)},x_{1}^{(4)},x_{2}^{(4)},x_{3}^{(4)},x_{4}^{(4)}\} =\{0,\frac{1}{3},\frac{1}{2},\frac{2}{3},1\}$
- $Q_{n}$ – kwadratura interpolacyjna

$$
\begin{align*}
Q_{n}(f) &= \sum\limits_{k=0}^{4}A_{k}^{(4)}f(x_{k}^{(4)})\\
A_{k}^{(4)} &= \int\limits_{0}^{1}\prod_{i=0,i\ne k}\frac{x-x_{i}^{(4)}}{x_{k}^{(4)}-x_{i}^{(4)}}dx
\end{align*}
$$
Teraz obliczamy na palcach:

- $A_{0} = A_{4} =  \frac{11}{120}$
- $A_{1} = A_{3} = \frac{27}{40}$
- $A_{2} = -\frac{8}{15}$

$$
Q_{n}(f) = \frac{11}{120}f(0) + \frac{27}{40}f\left(\frac{1}{3}\right) -\frac{8}{15}f\left(\frac{1}{2}\right) + \frac{27}{40}f\left(\frac{2}{3}\right) + \frac{11}{120}f(1)
$$

Można sprawdzić, że:

$$
\begin{align*}
f(x) = sin(2\pi x) \implies &\int\limits_{0}^{1}f(x)dx = \frac{2}{\pi} = 0.63661\dots\\
&Q_{n}(f) = \frac{27}{40}\sqrt{3} - \frac{8}{15} = \boxed{0.63}58\dots
\end{align*}
$$

$$
\begin{align*}
f(x) = e^{-x^{2}} \implies &\int\limits_{0}^{1}f(x)dx = 0.7468241\dots\\
&Q_{n}(f) = \boxed{0.7468}41\dots
\end{align*}
$$