## Definicja

Niech dane będą parami różne węzły $x_{0},x_{1},\dots$ oraz $(i \ne j \implies x_{i} \ne x_{j})$ oraz funkcja $f$ zdefiniowana w tych węzłach. Niech
$$
\begin{align*}
y_{k} &= f(x_{k}) &&(k = 0,1,2\dots)
\end{align*}
$$
Iloraz różnicowy funkcji $f$ w węzłach $x_{i},x_{i+1},\dots,x_{j}$ oznaczymy symbolem:
$$
f[x_{i},x_{i+1},\dots,x_{j}]
$$
i zdefiniujemy w następujący sposób:
$$
\begin{align*}
\begin{cases}
f[x_{i}] := f(x) = y_{i}\\
f[x_{i},x_{i+1},\dots,x_{j}] := \frac{f[x_{i+1,\dots,x_{j}}] - f[x_{i},\dots,x_{j-1}]}{x_{j}-x_{i}}
\end{cases}
\end{align*}
$$

## Wyznaczanie Ilorazów Różnicowych

Zauważmy, że kolejne ilorazy różnicowe możemy zapisać w tabelce:

$$
\begin{array}{c|c c}
x_{0} & y_{0} \\
x_{1} & y_{1} & f[x_{0},x_{1}]\\
x_{2} & y_{2} & f[x_{1},x_{2}] & f[x_{0},x_{1},x_{2}]\\
\vdots & \vdots & \vdots & \vdots & \ddots\\
x_{n} & y_{n} & f[x_{n-1},x_{n}] & f[x_{n-2},x_{n-1},x_{n}] & \dots & f[x_0,\dots,x_{n}]\\
\hline
x_{n+1} & y_{n+1} & f[x_{n},x_{n+1}] & f[x_{n-1},x_{n},x_{n+1}] & \dots & f[x_{1},\dots,x_{n+1}] & f[x_{0},\dots,x_{n+1}]
\end{array}
$$
