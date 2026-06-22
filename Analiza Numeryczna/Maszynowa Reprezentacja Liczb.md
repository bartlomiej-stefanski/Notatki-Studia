
> Tutaj rozpatrywany jest uproszczony model teoretyczny – [[Float IEEE 754]] na ćwiczeniach

## Liczby Całkowite

$$
l \in \mathbb{Z} : l = \pm \sum_{k = 0}^{n} e_{k}2^{k},\ \ \ e_{k}\in {0,1},\ \ e_{0} = 1
$$
Jeśli $n \ge d$ wystąpi nadmiar i przepełnienie.

## Liczby Rzeczywiste

$$
\begin{align*}
(x \ne 0)\ \ \ \ &x=s \cdot m \cdot 2^{c} \\
& s \in{\left\{+1,-1\right\}} \tag{znak liczby} \\
& m \in \left[\frac{1}{2},1\right) \tag{mantysa} \\
& c \in \mathbb{Z} \tag{cecha}
\end{align*}
$$

> Pokazać w domu, że reprezentacja jest zawsze jednorodna

#### Reprezentacja Mantysy

$$
m = \sum_{i=1}^{\infty}e_{-i}\cdot2^{-i},\ \ \ e_{i} \in \{0,1\}, e_{1} = q
$$

**Problem:**
Jak reprezentować mantysę biorąc pod uwagę że *prawie zawsze* reprezentacja dwójkowa *jest nieskończona?*

### Sposoby Zaokrąglania Mantysy

W rzeczywistości będziemy mieć tylko $t$ bitów, w których będziemy mogli zapisać informacje o mantysie, stąd *przybliżoną* mantysę będziemy określać $m_{t}$.

$$
\tiny\begin{split}
&\begin{array}{|c|c|c|c|c|c|c|c|}
\hline
  \pm & m_{t-1} & m_{t-2} & \dots & m_{1} & m_{0} & \pm & & \dots & \\
\hline
\end{array}
\\
& \text{t bitów mantysy}
\end{split}
$$

#### Obcięcie

Pamiętamy jedynie pewien prefix bitów liczby:
$$
m_{t} \equiv m_{t}^{c} \implies e_{-i}^{*} = e_{-i}\text{ dla } i=1,2,\dots,t
$$
#### Zaokrąglanie Symetryczne

Pamiętamy prefix bitów liczby i próbujemy zakodować informacje o jeszcze następnym bicie:
$$
m_{t} = m_{t}^{r} = \sum_{i=1}^{t}e_{-i}\cdot2^{-i} + e_{-(t+1)}\cdot2^{-t}
$$
>Jak wyglądają cyfry reprezentacji mantysy $e_{-i}^{x}$ przy zaokrągleniu symetrycznym?

### Maszynowa Reprezentacja Liczby Rzeczywistej $\ne0$

#### Cięcie

Zapamiętujemy tyle cyfr ile można:

$$
chop(x) = s \cdot m_{t}^{c}\cdot 2^{c}
$$
**Twierdzenie:**
Dla $x \ne 0$:
$$
\left|\frac{x - chop(x)}{x} \right| \le 2 \cdot 2^{-t}
$$


#### Zaokrąglenie Symetryczne

$$
rd(x) = s \cdot m_{t}^{r}\cdot 2^{c}
$$

**Twierdzenie:**
Dla $x \ne 0$:
$$
\left|\frac{x - rd(x)}{x} \right| \le 1 \cdot 2^{-t}
$$

---

> Jakie liczby, tzn. z jakiego zakresu, można reprezentować na komputerze?

$$
\text{maksymalna cecha} \rightarrow c_{max} = -c_{min} = 2^{d-t-1} - 1
$$
Teraz dla liczby $D = 2^{c_{max}}$ możemy reprezentować liczby z zakresu:
$$
\frac{1}{2D} \le |x| < D
$$
Przy czym przedział ten nie jest ciągły – będziemy potrafili zapamiętać w komputerze tylko niektóre liczby z tego przedziału:
$$
\begin{split}
X_{fl}& = rd(X) \\
X_{fl}& := \text{zbiór dyskretny} \\
X& := \text{zbiór ciągły}
\end{split}
$$

## Przykład

Rozważmy arytmetykę dla $d = 5, t = 3$:

$$
\tiny\begin{split}
&\begin{array}{|c|c|c|c|c|c|c|c|}
\hline
  \pm & 1 & ? & ? & \pm & ? \\
\hline
  b_{5} & b_{4} & b_{3} & b_{2} & b_{1} & b_{0} \\
\hline
\end{array} 
\end{split}
$$

Gdzie:
- $b_{5}$ – znak liczby
- $b_{4\dots2}$ – mantysa liczby
- $b_{1\dots0}$ – cecha liczby
