Macierz:
$$
\begin{align*}
A &= \begin{bmatrix}
a_{1,1} & a_{1,2} & a_{1,3} & \dots & a_{1,m}\\
a_{2,1} & a_{2,2} & a_{2,3} & \dots & a_{2,m}\\
a_{3,1} & a_{3,2} & a_{3,3} & \dots & a_{3,m}\\
\vdots & \vdots & \vdots & \ddots & \vdots\\
a_{n,1} & a_{n,2} & a_{n,3} & \dots & a_{n,m}
\end{bmatrix} \in \mathbb{R}^{n\times m}\\
\\
A &= [a_{i,j}]\in\mathbb{R}^{n\times m}, [a_{i,j}]_{n\times m}\\
\end{align*}
$$
Wektor: $b = \begin{bmatrix} b_{1}\\ b_{2} \\ \vdots \\ b_{n} \end{bmatrix} \in \mathbb{R}^{n\times 1} = \mathbb{R}^{n}$

### Operacje Na Macierzach

$$
\begin{align*}
& A = [a_{i,j}], B = [b_{i,j}] \in \mathbb{R}^{n\times m}\\
(\alpha \in \mathbb{R})\ \ \ \ \ \  & \alpha A = [\alpha\cdot a_{i,j}]\\
& A \pm B = [a_{i,j} \pm b_{i,j}] \in \mathbb{R}^{n\times m}
\end{align*}
$$

### Mnożenie Macierzy

$$
\begin{align*}
A &= [a_{i,j}] \in \mathbb{R}^{n\times k}\\
B &= [b_{i,j}] \in \mathbb{R}^{k\times n}\\
& \Downarrow\\
A\cdot B &= C = [c_{i,j}]\in\mathbb{R}^{k\times m}\\
c_{i,j} &= \sum\limits_{t=1}^{k}a_{i,t}\cdot b_{t,j}
\end{align*}
$$
### Macierz Identycznościowa

$$
\begin{align*}
\mathbb{R}^{n\times n} = I_{n} &= \begin{bmatrix}
1\\
& 1\\
& & \ddots \\
& & & 1
\end{bmatrix}\\
\\
\forall_{A\in\mathbb{R}^{n\times n}}\ I_{n}\cdot A &= A \cdot I_{n}
\end{align*}
$$

### Transpozycja Macierzy

$$
\begin{align*}
A = [a_{i,j}] \in \mathbb{R}^{n\times m} : A^{T}=[a_{j,i}]\in\mathbb{R}^{m\times n}
\end{align*}
$$

### Wyznacznik Macierzy

$$
\begin{align*}
&\text{def}: \mathbb{R}^{n\times n} \rightarrow\mathbb{R}\\\\
&\det(A) = \det\left(\begin{bmatrix}
a_{11} & \dots & a_{1,n}\\
\vdots & & \vdots\\
a_{n,1} & \dots & a_{n,n}\\
\end{bmatrix}\right) = \left|\begin{matrix}
a_{11} & \dots & a_{1,n}\\
\vdots & & \vdots\\
a_{n,1} & \dots & a_{n,n}\\
\end{matrix} \right|
\end{align*}
$$

##### Dla małych wartości proste...

- $|a_{1,1}| = a_{1,1}$
- $\left|\begin{matrix}a_{1,1} & a_{1,2}\\ a_{2,1} & a_{2,2}\end{matrix}\right| = a_{1,1}\cdot a_{2,2} - a_{1,2}\cdot a_{2,1}$
- Dla $\mathbb{R}^{3\times3}$ *sumujemy skosy* – jakiś ładny rysunek do tego znaleźć

##### Co dla $n\ge4$?

Gaussem można sprowadzić do macierzy trójkątnej, a wtedy wyznacznik można policzyć mnożąc elementy na przekątnej.

Do przekształceń używając Gaussa skorzystamy z faktu, że:

- $\det(A) = \det(A^{T})$
- $\det(A\cdot B) = \det(A)\cdot\det(B)$

### Macierz Odwrotna

Dla macierzy $A=[a_{i,j}]\in\mathbb{R}^{n\times n}$ będzie to taka macierz $B=[b_{i,j}]\in\mathbb{R}^{n\times n}$, że:
$$
A\cdot B = B\cdot A = I_{n}
$$
Wtedy oznaczamy $B\equiv A^{-1}$

##### Czy Macierz Odwrotna Zawsze Istnieje?

**Twierdzenie:** Macierz odwrotna do $A$ istnieje $\iff \det(A) \ne 0$.

##### Jak Znajdować Macierz Odwrotną?

To będzie trudne – nie chcemy szkolnej metody z wartościami własnymi, bo to za wolne.
Okaże się, że istnieje algorytm w $O(n^{3})$.

### Równania Liniowe

Dla danych:
- $A=[a_{i,j}]\in\mathbb{R}^{n\times n}$
- $b = \begin{bmatrix}b_{1}\\ b_{2} \\ \vdots \\ b_{n} \end{bmatrix} \in \mathbb{R}^{n}$
- $x = \begin{bmatrix}x_{1}\\ x_{2} \\ \vdots \\ x_{n} \end{bmatrix} \in \mathbb{R}^{n}$
Równanie w postaci $Ax = b$ można zapisać jako:
$$
\begin{align*}
\begin{cases}
a_{11}x_{1} + a_{1,2}x_{2} + a_{1,3}x_{3} + a_{1,n}x_{n} &= b_{1}\\
a_{21}x_{1} + a_{2,2}x_{2} + a_{2,3}x_{3} + a_{2,n}x_{n} &= b_{2}\\
\vdots & \vdots\\
a_{n1}x_{1} + a_{n,2}x_{2} + a_{n,3}x_{3} + a_{n,n}x_{n} &= b_{n}
\end{cases}
\end{align*}
$$

#### Kiedy Układ Równań Ma Dokładnie Jedno Rozwiązanie?

Wtedy, gdy $\det(A) \ne 0$.

$$
\begin{align*}
Ax &= b && | \cdot_{l} A^{-1}\\
A^{-1}(Ax) &= A^{-1}b\\
(A^{-1}A)x &= A^{-1}b\\
x &= \boxed{A^{-1}b}\\
\\
x_{k}&= \frac{\det(A_{k})}{\det(A)} && (1\le k \le n)
\end{align*}
$$
#### Przykład

$A = \begin{bmatrix}1 & 0.99 \\ 0.99 & 0.98\end{bmatrix}, b = \begin{bmatrix}1.99\\ 1.97\end{bmatrix}, \ \ \ \ \ \tilde{b} = b + \begin{bmatrix}-0.000037\\ +0.000106\end{bmatrix}$

Rozważmy dwa układy równań: $Ax = b$ i $Ax = \tilde{b}$.

- Rozwiązaniem układu $Ax = b$ jest $x = \begin{bmatrix}1 \\ 1\end{bmatrix}$
- Rozwiązaniem układu $Ax = \tilde{b}$ jest $\tilde{x} = \begin{bmatrix}3.00000 \\ -1.0203\end{bmatrix}$

**Wniosek:**
Rozwiązywanie nawet niewielkich układów równań może być [[Problemy Źle Uwarunkowane|źle uwarunkowane]].

