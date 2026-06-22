> Średniokwadratowa $\equiv$ śr□

Będziemy przybliżać dane ze zbioru dyskretnego *prostą* funkcją w taki sposób, by możliwe było szybkie wyznaczanie przybliżonych danych punktu.
Użyjemy kompresji *stratnej* – zapomnimy o niektórych danych.

### Jak Określić Bliskość Funkcji?

$f(x) = x$ i $g(x) = x + sin(x)$:
![[plot-x-and-xsinx.png]]

Najprostszym pomysłem na policzenie różnicy będzie po prostu całka:
$$
\int_{a}^{b}|f(x)-g(x)|dx
$$
Ale to jest niewykonalne, bo nie potrafimy całkować (numerycznie i normalnie).
Moduł we wzorze również nie pomaga...

---

Kolejny pomysł to wzięcie max z różnicy: $\max\limits_{a\le x\le b}|f(x)-g(x)|$, ale do tego potrzebna była by pochodna (trudne) i znalezienie miejsca zerowego pochodnej (znowu trudne).

---

> Po co nam to?

Będziemy chcieli znaleźć *prostą funkcję* bliską jakiejś *skomplikowanej funkcji* i mieć narzędzie do sprawdzenia jak dobrze wybraliśmy

## Norma Śr□

> Nieformalnie i tylko trochę: *miara wielkości funkcji*

Niech dana będzie funkcja $f$ określona na zbiorze $x_{0}<x_{1}<\dots<x_{N}$. Normę śr□ funkcji $f$ oznaczamy przez $||f||_{2}$ i oznaczamy wzorem:
$$
||f||_{2} = \sqrt{\sum\limits_{k=0}^{N}(f(x_{k}))^{2}}
$$
> Pierwiastek jest potrzebny, żeby to była norma (wymagana nierówność trójkąta)

#### Odległość śr□ Między Funkcjami

$f,g$ – funkcje określone na $x_{0}<x_{1}<\dots<x_{N}$, wtedy odległością będzie:
$$
||f-g||_{2}=\begin{cases}
\text{"małe"} &\Rightarrow\text{funkcje bliskie} \\
\text{"duże"} &\Rightarrow\text{funkcje dalekie}
\end{cases}
$$

##### Własności Normy śr□

- $||f||_{2} \ge 0$
	- $||f||_{2} = 0 \iff \forall_{i} f(x_{i}) = 0$
- $||\alpha \cdot f||_{2} = |\alpha|\cdot||f||_{2}$
- $||f+g||_{2}\le||f||_{2} + ||g||_{2}$

## Zadanie Aproksymacji śr□ na Zbiorze Dyskretnym

Dla danej funkcji $f$ określonej na zbiorze $x_{0}<x_{1}<\dots<x_{N}$ znaleźć taką funkcję
$\omega^{*}\in\mathscr{X}$ (ustalonym zbiorze funkcji *prostych*), aby:
$$
\begin{align*}
||f-\omega^{*}||_{2} = \min_{\omega\in\mathscr{X}}||f-\omega||_{2} = \min_{\omega\in\mathscr{X}}\sqrt{\sum\limits_{k=0}^{N}(f(x_{k}) - \omega(x_{k}))^{2}}
\end{align*}
$$
Jest to *błąd aproksymacji*.

> Pierwiastek jest monotoniczny, więc podczas liczenia można go pominąć

---
### Funkcja Stała

Model $\mathscr{X}\in\prod_0$:
$$
\begin{align*}
\min_{\omega\in\mathscr{X}}\sqrt{\sum\limits_{k=0}^{N}(f(x_{k})-\omega(x_{k}))^{2}} \leadsto \min_{a\in\mathbb{R}}\sum\limits_{k=0}^{N}(f(x_{k})-a)^{2} \leadsto E'(a)=0\\
\\
E'(a) = -2\sum\limits_{k=0}^{N}(f(x_{k})-a) = 0 \iff \boxed{a=\frac{\sum\limits_{k=0}^{N}f(x_{k})}{N+1}}
\end{align*}
$$
Otrzymujemy kandydata na ekstremum.

> Dlaczego w tym punkcie jest minimum?

$(f(x_{k})-a)^{2}$ jest funkcją kwadratową z ramionami skierowanymi do góry, stąd posiada jedno ekstremum, które będzie minimum.

### Funkcja Kwadratowa

Model $\mathscr{X} = \{ax^{2} : a\in\mathbb{R}\}$:
$$
\begin{align*}
\min_{\omega\in\mathscr{X}}\sqrt{\sum\limits_{k=0}^{N}(f(x_{k})-\omega(x_{k}))^{2}} \leadsto \min_{a\in\mathbb{R}}\sum\limits_{k=0}^{N}(f(x_{k})-ax_{k}^{2})^{2} = 0 \leadsto E'(a) = 0\\
\\
E'(a) = -2\sum\limits_{k=0}^{N}(f(x_{k})-ax_{k}^{2})x_{k}^{2} = 0 \iff \boxed{a=\frac{\sum\limits_{k=0}^{N}f(x_{k})x_{k}^{2}}{\sum\limits_{k=0}^{N}x_{k}^{4}}}
\end{align*}
$$
Otrzymujemy minimum *funkcji błędu*.

**Wniosek:**
Element optymalny $\omega^{*}(x) \in \{ax^{2} : a \in \mathbb{R}\}$ jest postaci:
$$
\omega(x) = \left(\frac{\sum\limits_{k=0}^{N}f(x_{k})x_{k}^{2}}{\sum\limits_{k=0}^{N}x_{k}^{4}}\right)\cdot x^{2}
$$

*Obserwacja:*

Pojedyncze punkty odstające od reszty zostaną pominięte.

### Funkcja Liniowa

Model $\mathscr{X} = \prod_{1} = \{ax+b : a,b\in\mathbb{R}\}$:

![[Pochodne Cząstkowe#Ekstrema]]

$$
\begin{align*}
\min_{\omega\in\prod_{1}}\sqrt{\sum\limits_{k=0}^{N}(f(x_{k}) -\omega(x_{k}))^{2}} \leadsto \min_{a,b\in\mathbb{R}}\sum\limits_{k=0}^{N}(f(x_{k})-ax_{k}-b)^{2} = E(a,b)\\
\\
\leadsto\boxed{\frac{\partial E(a,b)}{\partial a} = 0, \frac{\partial E(a,b)}{\partial b} = 0}\\
\\
\begin{cases}
\frac{\partial E(a,b)}{\partial a} =-2\sum\limits_{k=0}^{N}(f(x_{k})-ax_{k}-b)x_{k}=0\\
\frac{\partial E(a,b)}{\partial b} = -2\sum\limits_{k=0}^{N}(f(x_{k})-ax_{k}-b)=0
\end{cases}
\iff
\begin{cases}
a\left(\sum\limits_{k=0}^{N}x_{k}^{2}\right)+b\left(\sum\limits_{k=0}^{N}x_{k}\right)=\sum\limits_{k=0}^{N}f(x_{k})x_{k}\\
a\left(\sum\limits_{k=0}^{N}x_{k}\right)+b(N+1)=\sum\limits_{k=0}^{N}f(x_{k})
\end{cases}
\end{align*}
$$
Otrzymujemy rozwiązywalny układ równań dwóch zmiennych z dwoma równaniami.

*Plot-twist:* To jest regresja liniowa.

### Ogólny Model Liniowy z Wieloma Parametrami

$g_{1}(x), g_{2}(x),\dots,g_{n}(x)$ – liniowo niezależne.
$$
\text{model} \rightarrow \mathscr{X} = \{\sum\limits_{i=1}^{n}a_{i}g_{i}(x) : a_{1},a_{2},\dots,a_{n}\in\mathbb{R}\}
$$
Szukamy $w^{*} \in \mathscr{X}$, dla którego:
$$
||f-\omega||_{2}=\min_{\omega\in\mathscr{X}}||f-\omega||_{2}=\min_{a_{1},\dots,a_{n}\in\mathbb{R}}\sqrt{\sum\limits_{k=0}^{N}\left(f(x_{k})-\sum\limits_{i=1}^{n}a_{i}g_{i}(x_{k})\right)^{2}}
$$
Stąd funkcja błędu:
$$
\begin{align*}
E(a_{1},a_{2},\dots,a_{n}) &= \sum\limits_{k=0}^{N}\left(f(x_{k})-\sum\limits_{i=1}^{n}a_{i}g_{i}(x_{k})\right)^{2}\\
\omega(x_{k}) &= \sum\limits_{i=1}^{n}a_{i}g_{i}(x_{k})\\
&\text{Układ równań normalnych:}\\
&\frac{\partial E(a_{1},\dots,a_{n})}{\partial a_{k}} = 0
\end{align*}
$$
Co jest układem równań liniowych z $n$ niewiadomymi.
Standardowy kosz rozwiązania będzie wynosił $O(m^{3})$ – dużo.

## Alternatywny Sposób Liczenia

> Tak naprawdę taki sam, tylko że może zrobiony *ładniej*.

Będziemy chcieli przybliżać funkcję $f$ pewną kombinacją liniową:
$$
w(x) = \alpha_{0}g_{0}(x) + \alpha_{1}g_{1}(x) + \dots
$$
Gdzie ~~funkcje~~ wektory liniowo niezależne: $g_{0},g_1,\dots$, więc $W = lin\{g_{0},g_{1},\dots\}$.

By odnaleźć wektor z podprzestrzeni $W$ *najbliższy* $f$, wykonamy *rzut prostopadły*.
Rzut prostopadły jest *prostopadły*, stąd:
$$
\begin{align*}
f-w \bot W&\iff \forall_{i}f-w \bot g_{i}\\
\end{align*}
$$
Stąd: 
$$
\forall_{i}<f-w,g_{i}>_{N}=0 \iff <w,g_{i}>_{N} = <f,g_{i}>_{N}
$$
Z tego otrzymujemy układ równań:
$$
\begin{align*}
\begin{bmatrix}
<g_{0},g_{0}>_{N} & <g_{1},g_{0}>_{N} & <g_{2},g_{0}>_{N}\\
<g_{0},g_{1}>_{N} & <g_{1},g_{1}>_{N} & <g_{2},g_{1}>_{N}\\
<g_{0},g_{2}>_{N} & <g_{1},g_{2}>_{N} & <g_{2},g_{2}>_{N}
\end{bmatrix}
\begin{bmatrix}\alpha_{0}\\ \alpha_{1}\\ \alpha_{2}
\end{bmatrix}
=
\begin{bmatrix}
<f,g_{0}>_{N} \\ <f,g_{1}>_{N} \\ <f,g_{2}>_{N}
\end{bmatrix}
\end{align*}
$$
Który będziemy potrafili *jakoś* rozwiązać

> Gdzie tu *kwadratowość*?

W iloczynie skalarnym.
#### Dyskretny Iloczyn Skalarny

$$
<f,g>_{N} = \sum\limits_{k=0}^{N}f(x_{k})g(x)k
$$
Jest to *porządny* iloczyn skalarny, więc zachodzi:

- $<f,g>_{N} = <g,f>_{N}$
- $<\alpha f, g>_{N} = \alpha <f,g>_{N}$
- $<f+g,h>_{N} = <f,h>_{N} + <g,h>_{N}$
- $<f,f>_{N}= ||f||_{2}^{2}$
- $f \bot g \iff <f,g>=0$

