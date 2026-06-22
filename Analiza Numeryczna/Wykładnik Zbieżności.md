## Definicja

Niech dany będzie ciąg $(x_{\alpha})$ zbieżny do $\alpha$. Jeżeli istnieją takie liczby rzeczywiste $p$ oraz $c > 0$, że:
$$
\lim_{n\to\infty}\frac{|x_{n+1} - \alpha|}{|x_{n}-\alpha|^{p}} =c
$$
to $p$ nazywamy *wykładnikiem zbieżności* ciągu $(x_{\alpha})$, a stałą $c$ stałą asymptotyczną.

> Dla zbieżności liniowej chcemy dodatkowo, by $c < 1$.
> Dla dowolnych wyższych rzędów stała okaże się nieistotna.

Jeśli $p = 1$ (to wtedy musi być też $c \in (0,1)$), to mówimy, że ciąg jest zbieżny liniowo. Jeżeli $p = 2$, to jest zbieżny kwadratowo, dla $p=3$ – sześcienna, ...

## Zbieżność Metody Newtona

### Pojedyncze Miejsce Zerowe

Niech $\alpha$ będzie pojedynczym ($f(\alpha) = 0 \ne f'(\alpha)$) miejscem zerowym funkcji $f(x)$.
Wtedy [[Rozwiązywanie Równań Liniowych#Metoda Newtona|Metoda Newtona]] (przy założeniu, że jest zbieżna dla wybranego $x_{0}$) ma wykładnik zbieżności $p = 2$ – jest to *zbieżność kwadratowa*. 

### Podwójne Miejsce Zerowe

Niech $\alpha$ będzie podwójnym ($f(\alpha) = 0 = f'(\alpha) \ne f''(\alpha)$) miejscem zerowym.
Wtedy [[Rozwiązywanie Równań Liniowych#Metoda Newtona|Metoda Newtona]] (jeśli zbiega), to Metoda Newtona jest metodą *rzędu pierwszego* – $p = 1$.

## Zbieżność Metody Siecznych

[[Rozwiązywanie Równań Liniowych#Metoda Siecznych|Metoda Siecznych]] w wypadku pierwiastków pojedynczych jest metodą rzędu $p = \frac{\sqrt{5} + 1}{2} \approx 1,618\dots < 2$, co jest gorszym wynikiem niż *Newton*.

---

## Znajdywanie Rzędu Metody

Rozważmy tak zwane *metody jedno-krokowe* – to jest metody postaci:
$$
\begin{cases}
x_{0} \rightarrow dane \\
x_{n+1} \rightarrow F(x_{n})
\end{cases}
$$
Tak wygląda np. *Metoda newtona*.

Rząd metody *jednokrokowej* jest liczbą naturalną $p$ wtedy i tylko wtedy, gdy:
$$
F(\alpha) = 0, F'(\alpha) = 0,\dots,F^{(p-1)}(\alpha) = 0 \land \boxed{F^{(p)}(\alpha) \ne 0}
$$
gdzie $\alpha = \lim\limits_{n\to\infty}x_{n}$, natomiast stała asymptotyczna $c = \frac{F^{(p)}(\alpha)}{p!}$.
