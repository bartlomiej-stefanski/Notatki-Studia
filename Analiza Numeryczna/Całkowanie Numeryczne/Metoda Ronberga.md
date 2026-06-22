> Dla chętnych *ekstrapolacja Richardsona*

Niech $n=2^{k}, k\in\mathbb{N}$ i niech:

- $h_{k}=\frac{b-a}{2}$
- $x_{i}^{(k)} = a + ih_{k}$
- $T_{0,k}= T_{2^{k}}(f) = {\sum\limits_{i=0}^{2^{k}}}'' f(x_{i}^{(k)})$ – to jest wzór trapezów
$$
\boxed{T_{m,k} =\frac{4^{m}T_{m-1,k+1} - 1T_{n-1,k}}{4^{m}-1}}\longleftarrow\text{metoda Ronberga}
$$

### Tablica Romberga

Czyli jak realizować wzór w praktyce.
$$
\begin{align*}
\begin{array}{c | c c}
T_{0,0}\\
& \searrow \\
T_{0,1} & \rightarrow & T_{1,0}\\
& \searrow & & \searrow\\
T_{0,2} & \rightarrow & T_{1,1} & \rightarrow & T_{2,0}\\
& \searrow & & \searrow & & \searrow\\
T_{0,3} & \rightarrow & T_{1,2} & \rightarrow & T_{2,1} & \rightarrow & T_{3,0}\\
\vdots & &\vdots & & \vdots & &\vdots
\end{array}
\end{align*}
$$
Głównym kosztem będzie policzenie wszystkich $T_{0,i}$.
Będziemy chcieli liczyć wartości funkcji w każdym punkcie tylko raz, w celu czego skorzystamy z faktu, że $T_{2^{m+1}} \leadsto T_{2^{m}}$, ale to na ćwiczeniach.

### Jakieś Losowe Własności

Ale za trudne dla nas żeby je dowodzić...

- $T_{m,k} = \int\limits_{a}^{b}f(x)dx + O(h_{k}^{2m+2})$
- $T_{m,k} = \sum\limits_{j=0}^{2^{m+k}}A_{j}^{(m)}f(x_{j}^{(m+k)})$ – współczynniki $A_{j}^{(n)} > 0$
- $T_{m,0}, T_{m,1}, T_{m,2},\dots$ to kwadratury rzędu $2n+2$
