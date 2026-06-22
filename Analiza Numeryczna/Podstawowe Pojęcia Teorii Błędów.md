 $$
 \begin{split}
x = 1.23456789 \rightarrow & \widetilde{x} = 1.2345679 \\
y = 10^{50}+1 \rightarrow & \widetilde{y} = 10^{50}
\end{split}
$$

## Błędy bezwzględne:

$$
\mid x - \widetilde{x}\mid = \boxed{10^{-8}}\ \ \ \ \ \mid y - \widetilde{y} \mid = \boxed{1}
$$

## Błędy względne:

$$
\frac{\mid x - \widetilde x\mid}{\mid x \mid} \approx \boxed{0.8 * 10^{-8}}\ \ \ \ \ \frac{\mid y - \widetilde{y}\mid}{\mid y \mid} \approx \boxed{10^{-50}}
$$

## Liczba cyfr dokładnych:

$$
acc(v,\widetilde{v}) = -log_{10}{\left|\frac{v-\widetilde{v}}{v}\right|}
$$
Teraz przykład:
$$
acc(x,\widetilde{x}) = 8.09\ \ \ \ \ \ acc(y,\widetilde{y}) = 50
$$
