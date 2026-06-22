Układ trójkątny Dolny:
$$
\begin{align*}
\begin{cases}
l_{1,1}x_{1} &= b_{1}\\
l_{2,1}x_{1} + l_{2,2}x_{2} &= b_{2}\\
l_{3,1}x_{1}+ l_{3,2}x_{2} + l_{3,3} &= b_{3}\\
\vdots\\
l_{n,1}x_{1} + l_{n,2}x_{2} + l_{n,3}x_{3} + \dots +l_{n,n}x_{n} &= b_{n}
\end{cases}\\
\\
\boxed{x_{k} = \frac{b_{k}-\sum\limits_{j=1}^{k-1}l_{k,j}x_{j}}{l_{k,k}}}
\end{align*}
$$
Rozwiązywalny standardowo w czasie $O(n^{2})$.

Bardzo podobnie można rozwiązać układ jeśli będzie górnotrójkątny.

#### Zapis Macierzowy

- $L = \begin{bmatrix}L_{1,1}\\ L_{2,1} & L_{2,2}\\ L_{3,1} & L_{3,2} & L_{3,3}\\ \vdots& \vdots& \vdots& \ddots\\ l_{n,1} & l_{n,2} & l_{n,3} & & l_{n,n}\end{bmatrix}\equiv ◺$
- $U = \begin{bmatrix}u_{1,1} & u_{1,2} & u_{1,3} & \dots & u_{1,n}\\ & u_{2,2} & u_{2,3} & \dots & u_{2,n} \\ & & u_{3,3} & \dots & u_{3,n} \\ & & & \ddots & \vdots\\ & & & & u_{n,n}\end{bmatrix}\equiv ◹$

> Odpowiednio **L**ower i **U**pper

## Metoda Faktoryzacji

Niech dany będzie układ równań postaci:
$$
\begin{align*}
Ax = b &&(A\in\mathbb{R}^{n\times n}; x,b\in\mathbb{R}^{n})
\end{align*}
$$
Załóżmy, że znamy takie macierze $L = ◺, U = ◹ \in\mathbb{R}^{n\times n}$, że $A = L\cdot U$.

Wtedy *faktyczna* metoda faktoryzacji:
$$
\begin{align*}
Ax &= b\\
(L\cdot U)x &= b\\
L(U\cdot x) &= b && \text{niech } Ux = y\\
Ly &= b && \text{Policzymy y}\\
Ux &= y && \text{Policzymy x}
\end{align*}
$$
Policzenie $x$ i $y$ będzie tanie, bo pracujemy na macierzach $\triangle$.

#### Czy Zawsze Istnieją L i U?

Nie zawsze, ale więcej o tym za tydzień...

#### Jak Znaleźć Rozkład Jeśli Istnieje?

**Twierdzenie:** (o rozkładzie trójkątnym macierzy)
Niech dana będzie macierz $A\in\mathbb{R}^{n\times n}$, dla której wszystkie *minory główne* są różne od zera, czyli:
$$
\begin{align*}
\left|\begin{matrix}
a_{1,1} & a_{1,2} & \dots & a_{1,n}\\
a_{2,1} & a_{2,2} & \dots & a_{2,n}\\
\vdots & \vdots & \ddots & \vdots\\
a_{k,1} & a_{k,2} & \dots & a_{k,k}
\end{matrix}\right| \ne 0 && (k=1,2,\dots,n)
\end{align*}
$$
Wtedy istnieje dokładnie jedna para $L=[l_{i,j}],U=[u_{i,j}]$ takich, że $A=L\cdot U$.
Gdzie $l_{i,i} = 1$, czyli macierz $L$ ma jedynki na przekątnej.
Wtedy takie macierze można wyznaczyć:
$$
\begin{align*}
u_{i,j} &= a_{i,j}-\sum\limits_{k=1}^{i-1}l_{i,k}\cdot u_{k,j} &&(i \le j)\\
l_{i,j} &= \frac{a_{i,j}-\sum\limits_{k=1}^{j-1}l_{i,k}\cdot u_{k,j}}{u_{j,j}}
\end{align*}
$$
> W jakiej kolejności wykonywać działania?
> O tym na ćwiczeniach.

### Podsumowanie

Rozwiązanie układu równań metodą faktoryzacji ma następującą złożoność obliczeniową:

- Znalezienie rozkładu LU: $O(n^{3})$
- Rozwiązanie układu trójkątnego: $O(n^{2})$

### Inne Zastosowanie Rozkładu LU

- Obliczanie wyznacznika macierzy: $\det(A) = \det(L\cdot U) = \det(L)\cdot\det(U)$.
  Macierze są trójkątne więc łatwe do policzenia.
- Odwracanie macierzy: $A^{-1} = (L\cdot U) = U^{-1} \cdot L^{-1}$.
  Wystarczy więc umieć odwracać macierze trójkątne.

> Zadanie domowe: Jak odwracań macierze trójkątne?
