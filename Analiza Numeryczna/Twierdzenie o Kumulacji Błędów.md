> Twierdzenie do użycia przy analizie zmiennopozycyjnej realizacji algorytmów

Jeśli
$$
\begin{split}
|\delta_{i}| &\le 2^{-t}\ \ \ \ \ (i=1,2,\dots,n),a \\
\prod_{i=1}^{n}(1+\delta_{i}) &= 1 + \sigma_{n} \\
\end{split}
$$
To:
$$
\sigma_{n} = \boxed{\sum_{i=1}^{n}\delta_{i}} + O(2^{-2t})
$$

Jeśli $n \cdot 2^{-t} < 2$, to:
$$
\begin{split}
|\sigma_{n}| \le \gamma_{n} = \frac{n \cdot 2^{-t}}{1-\frac{1}{2}n\cdot2^{-t}}& \approx n \cdot 2^{-t} \\
 & \Downarrow\\
|\sigma_{n}| &\lesssim  n \cdot 2^{-t}
\end{split}
$$


## Przykład

Sumujemy liczby $x_{1},x_{2},x_{3},x_{4},x_{5}$ w naturalnej kolejności w arytmetyce zmiennopozycyjnej:

```
S := x[1]
for i := 2 to 5:
    S = S + x[i]

return(s)
```

Założenie: $x_{i} = rd(x_{i})$.

$$
\begin{split}
fl(S) =&\ ((((x_{1} + x_{2})(1+\epsilon_{2}) + x_{3})(1 + \epsilon_{3}) + x_{4})(1 + \epsilon_{4}) + x_{5})(1+\epsilon_{5}) \\
 =&\ x_{1}(\epsilon_{2} + 1)(\epsilon_{3} + 1)(\epsilon_{4} + 1)(\epsilon_{5} + 1)  + \\
  &\ x_{2}(\epsilon_{2} + 1)(\epsilon_{3} + 1)(\epsilon_{4} + 1)(\epsilon_{5} + 1) + \\
  &\ x_{3}(\epsilon_{3} + 1)(\epsilon_{4} + 1)(\epsilon_{5} + 1)+\\
  &\ x_{4}(\epsilon_{4} + 1)(\epsilon_{5} + 1)+\\
  &\ x_{5}(\epsilon_{5} + 1)\\
  =&\ \sum_{i=1}^{5}x_{i}(1 + E_{i})
\end{split}
$$
Gdzie:
$$
\begin{split}
1+E_{k} &= \prod_{i=k}^{5}(1+\epsilon_{i}) \\
|E_{1}| &\lesssim \cdot2^{-t}\\
|E_{2}| &\lesssim 2\cdot2^{-t}\\
|E_{3}| &\lesssim 3\cdot2^{-t}\\
|E_{4}| &\lesssim 4\cdot2^{-t}\\
|E_{5}| &\lesssim 5\cdot 2^{-t}\\
|E_{k}| &\lesssim \text{tw. kumulacja błędów}
\end{split}
$$

#### Błąd Względny

$$
\begin{split}
\left| \frac{S-fl(S)}{S} \right| = \left| \frac{\sum_{i}x_{i}E_{i}}{\sum_{i}x_{i}} \right| \le \frac{\sum_{i}|x_{i}||E_{i}|}{|\sum_{i}x_{i}|} \lesssim 4\cdot2^{-t} \frac{\sum_{i}|x_{i}|}{|\sum_{i}x_{i}|}
\end{split}
$$
Wnioski:

- Jeśli liczby są tego samego znaku, to będzie OK
- Jeśli są różnych znaków, to $|\sum_{i}x_{i}|$ może być dowolnie małe – błąd zmierza do nieskończoności (trochę źle)