Niech ciąg $\phi_{k},\ k=0,1,\dots$ spełnia liniową relację rekurencyjną
$$
\begin{align*}
\phi_{k+1}(x) + \alpha_{k}(x)\phi_{k}(x) + \beta_{k}(x)\phi_{k-1}(x) &= 0
\end{align*}
$$
gdzie współczynniki $\alpha_{k},\beta_{k}$ są znane.
Dla dowolnego skończonego ciągu $c_{0},\dots,c_{n}$ definiujemy $b_{k}$ przez *odwrócony* wzór rekurencyjny:
$$
\begin{align*}
b_{n+1}(x) &= b_{n+2}(x) = 0\\
b_{k}(x) &= c_{k} - \alpha_{k}(x)b_{k+1}(x) - \beta_{k+1}(x)b_{k+2}(x)
\end{align*}
$$
wtedy kombinacja liniowa $\phi_{k}$ spełnia:
$$
\begin{align*}
\sum\limits_{k=0}^{n}c_{k}\phi_{k}(x) &= b_{0}(x)\phi_{0}(x)+b_{1}(x)\cdot(\phi_{1}(x) + \alpha_{0}(x)\phi_{0}(x))
\end{align*}
$$