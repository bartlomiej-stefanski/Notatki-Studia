Niech dane będą punkty $W_{k}=\mathbb{E}^{2} (k=0,1,\dots,n)$
Krzywą parametryczną postaci:
$$
\begin{align*}
\text{dla } t\in[0,1]: P_{n}(t) = B_{0}^{n}(x)W_{0} + B_{1}^{n}(x)W_{1} + \dots+B_{n}^{n}(x)W_{n}
\end{align*}
$$
Nazywamy krzywa Béziera stopnia $n$, punkty $W_{k}$ jej punktami kontrolnymi.

Zauważmy, że $P(t)$ dla dowolnego $t$ jest *kombinacją barycentryczną* punktów kontrolnych, czyli punktem na płaszczyźnie $P : [0,1] \rightarrow \text{ punkt w }\mathbb{E}^{2}$.

Podstawowe własności:
- $P(0) = W_{0}$
- $P(1) = W_{n}$
- $P([0,1]) = \text{conv}\{w_{0},w_{1},\dots,w_{n}\}$

### Algorytm de Casteljau

![[de-castlejau-bezier-calculation.png]]

Niech dana będzie krzywa Béziera $P(t)$ o punktach kontrolnych $W_{k}\in\mathbb{E}^{2}\ (0,1,\dots,n)$, oraz liczba $t\in[0,1]$.

Niech wielkości $W_{k}^{(i)}$ dla $(i = 0,1,\dots,n; k=0,1,\dots,n-1)$ będą określone w następujący sposób:

- $W_{k}^{(0)} = W_{k}$
- $W_{k}^{(i)} = (1-t)W_{k}^{(i-1)}+ tW_{k+1}^{(i-1)}$ 

Wtedy $P(t) = W_{0}^{(n)}$.
Złożoność tego algorytmu to $O(n^{2})$.

> Czy można szybciej?

Tak $\implies$ schemat Hornera $\implies$ $P(t)$ obliczamy w czasie $O(n)$.
Wcale na pewno nie będzie na egzaminie...

## Transformacja Krzywych Béziera

### Prostsza Wersja – Krzywe Tego Samego Stopnia

$$
\begin{align*}
&\begin{cases}
P_{n}(t) = \sum\limits_{k=0}^{n}B_{k}^{n}(t)W_{k}\\
R_{n}(t) = \sum\limits_{k=0}^{n}B_{k}^{n}(t)V_{k}
\end{cases}
\overset{transform}{\implies}
S_{n}^{\infty}(t) = (1-\alpha)P_{n}(t) + \alpha R_{n}(t), \alpha\in[0,1]\\
\\
&S_{n}^{\infty}(t) = \sum\limits_{k=0}^{n}B_{k}^{n}(t)[(1-\alpha)W_{k} + \alpha V_{k}]\\
&\text{Nowe punkty są postaci: }(1-\alpha)W_{k} + \alpha V_{k}
\end{align*}
$$
Tak zdefiniowana krzywa również jest krzywą Béziera.

### Krzywe Różnego Stopnia

Będziemy chcieli *dodać* punkty do krzywej niższego stopnia, by miała tyle punktów, co krzywa wyższego stopnia.
Proces taki nazwiemy *podnoszeniem stopnia*.

**Narzędzie:**
$$
\begin{align*}
B_{k}^{n}(t) = \frac{n-k+1}{n+1}B_{k}^{n+1}(t) + \frac{k+1}{n+1}B_{k+1}^{n+1}(t)
\end{align*}
$$

### Wymierna Krzywa Béziera

> Pojawiło się na ćwiczeniach, przydatne do projektu

$$
\begin{align*}
R_{n}(t) &= \frac{\sum\limits_{i=0}^{n}w_{i}W_{i}B_{i}^{n}(t)}{\sum\limits_{i=0}^{n}w_{i}B_{i}^{n}(t)}
\end{align*}
$$
Gdzie $W_{0},W_{1},\dots,W_{n}\in\mathbb{E}^{2}$ są punktami kontrolnymi, a $w_{0},w_{1},\dots,w_{n}\in\mathbb{R}_{+}$ wagami.

Dla wszystkich $t\in[0,1]$ wartości $R_{n}(t)$ są [[Wielomiany Bernsteina#Kombinacja Barycentryczna|Kombinacją Barycentryczną]].
