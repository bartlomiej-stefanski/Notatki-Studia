Jak skonstruować [[Kwadratura Liniowa|kwadraturę liniową]] $Q_{n}(f) = \sum\limits_{k=0}^{n}A_{k}^{(n)}f(x_{k}^{(n)})$, 
dla której rząd wynosi $2n+2$?

Będzie to na pewno [[Kwadratura Interpolacyjna|kwadratura interpolacyjna]], bo $2n+2 > n+1$, czyli:
$$
\begin{align*}
A_{k}^{(n)} &= \int\limits_{a}^{b}\left(\prod\limits_{\substack{i=0\\ i\ne k}}^{n}\frac{x-x_{i}^{(n)}}{x_{k}^{(n)} - x_{i}^{(n)}}\right)dx
\end{align*}
$$
Musimy dobrać węzły w taki sposób, aby $\boxed{\forall_{w\in\prod_{2n+1}}Q_{n}(w)=\int\limits_{a}^{b}w(x)dx}$.
### Twierdzenie

Przyjmijmy, że $[a,b]=[-1,1]$. Węzły $x_{0}^{(n)},x_{1}^{(n)},x_{2}^{(n)},\dots,x_{n}^{(n)}$ kwadratury liniowej mające rząd $2n+2$ są miejscami zerowymi tak zwanego $n+1$-szego wielomianu Legendre'a.
Wielomiany Legendre'a spełniają następujący związek rekurencyjny:
$$
\begin{align*}
\begin{cases}
P_{0}(x) = 1 \\
P_{1}(x) = x \\
P_{k}(x) = \frac{2k-1}{k}P_{k-1}(x) - \frac{k-1}{k}P_{k-2}(x)
\end{cases}
\end{align*}
$$
**Uwaga:**

1. Wielomiany Legendre'a wyznaczamy rekurencyjnie ze wzoru $(*)$
2. Nie ma jawnych wzorów dla miejsc zerowych tych wielomianów
3. Miejsca zerowe można z dużą dokładnością obliczać metodami numerycznymi
4. W praktyce by otrzymać miejsca zerowe tych wielomianów skorzystamy z obliczonych już przez kogoś miejsc zerowych

