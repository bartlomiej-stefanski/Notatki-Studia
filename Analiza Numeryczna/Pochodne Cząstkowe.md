Dotychczasowe modele zależały jedynie od *jednego parametru*.
Co zrobić gdy parametrów jest kilka? Użyć *pochodnych cząstkowych*:

$$
\begin{align*}
f(x,y) &= 3x^{4} + (5\cos(xy) - y^{2})^{3}\\
\\
\frac{\partial f(x,y)}{\partial x} &= 12x^{2}+3(5\cos(xy)-y^{2})^{2}\cdot(-5\sin(xy)y - 0)\\
\frac{\partial f(x,y)}{\partial y} &= 0 + 3(5\cos(xy) - y^{2})^{2}\cdot(-5\sin(xy)x - 2y)
\end{align*}
$$
Wykonując pochodną po wybranej zmiennej uznajemy wszystkie inne jako stałe.

**Ogólnie:**
Dla $f(x_{1},x_{2},\dots,x_{n})$ pochodna cząstkowa to: $\frac{\partial f(x_{1},\dots,x_{n})}{\partial x_{k}}$.

### Ekstrema

Niech dana będzie funkcja wielu zmiennych $f: \mathbb{R}^{n} \rightarrow \mathbb{R}$.
Warunkiem koniecznym istnienia ekstremum funkcji $f$ w punkcie $(x_{1},x_{2},\dots,x_{n})\in\mathbb{R}^{n}$ jest zerowanie się w tym punkcie wszystkich pochodnych cząstkowych funkcji $f$.