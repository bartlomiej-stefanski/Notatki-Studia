## Definicja

Zadanie nazywamy *źle uwarunkowanym*, jeśli **mała** względna zmiana *danych* powoduje **dużą** względną zmianę *wyniku*.

> Inaczej *efekt motyla* \[tu wstaw rysunek motyla z wykładu (był przepiękny, nie do odtworzenia, więc jednak nie ma)\]

#### Uwaga 1

Rozwiązując zadania źle uwarunkowane przy pomocy komputera i arytmetyki *fl* należy zachować szczególną ostrożność.  
Przy samym wprowadzaniu danych można już popełnić na tyle duży błąd, że wyniki będą bezwartościowe. 

#### Uwaga 2

Uwarunkowanie to cecha zadania i nie da się tego zmienić.

## Przykład 1

> Perfidny wielomian Wilkinsona

Zdefiniujmy wielomian:
$$
\begin{align*}
\omega(x) &=  (x-1)(x-2)\dots(x-20)\\
&= 1 \cdot x^{20} - 210 \cdot x^{19} + \dots\\
\omega_{\epsilon}(x) &= \omega(x) - \epsilon \cdot x^{19}
\end{align*}
$$
Już dla $\epsilon \approx 2 \cdot 10^{-30}$ wartości bardzo się rozjadą – wykres będzie zupełnie inny i część miejsc zerowych stanie się urojona.

**Wniosek:** problem jest źle uwarunkowany numerycznie.

## Przykład 2

> Perfidna macierz Hilberta

$$
\begin{align*}
H_{n} &=  \begin{bmatrix} \frac{1}{i+j-1} \end{bmatrix}_{n\times n} \tag{macierz Hilberta} \\
\widetilde{H}_{n} &= \begin{bmatrix} rd\left(\frac{1}{i+j-1}\right) \end{bmatrix}_{n \times n} \tag{numeryczna macierz Hilberta}
\end{align*}
$$

> *Numeryczna* – zapamiętujemy liczby najlepiej jak umiemy na komputerze.

Teraz policzmy:
$$
\begin{align*}
det(H_{15}) &\approx 0.10585427 \cdot 10^{-123}\\
det(\widetilde{H}_{15}) &= 0.47591091 \cdot 10^{-86}
\end{align*}
$$
Błąd względny wynosi $\approx 100\%$  
Oznacza to, że trzymane wyniki są zupełnie bez sensu.

**Wniosek:** problem jest źle uwarunkowany numerycznie.

## Przykład 3

Rozważmy następujący układ równań liniowych:
$$
\begin{align*}
H_{n} \begin{bmatrix} x_{1} \\ x_{2} \\ \vdots \\ x_{n} \end{bmatrix} &= b_{n}, \text{ gdzie rozwiązanie: } b_{n} = H_{n}\begin{bmatrix} 1 \\ 1 \\ \vdots \\ 1\end{bmatrix} \\
\widetilde{H}_{n} \begin{bmatrix} x_{1} \\ x_{2} \\ \vdots \\ x_{n} \end{bmatrix} &= fl(b_{n})
\end{align*}
$$
Oczekiwalibyśmy $x_{1}=x_{2}=\dots=x_{n}=1$, ale okaże się, że już dla małej zmiany danych w układzie równań dostaniemy rozwiązania dalekie od $1$.

**Wniosek:** problem jest źle uwarunkowany numerycznie.

## W Jaki Sposób Badać Uwarunkowanie Zadania?

Niestety ~~jest to trudne~~ *nie jest to łatwe*. Znowu czas na przykłady.

### Wskaźnik Uwarunkowania Funkcji Jednej Zmiennej

Zbadamy uwarunkowanie zadania *obliczania wartości* **ustalonej** funkcji.
$$
\begin{align*}
\left| \frac{x - (x + h)}{x} \right| &= \left| \frac{h}{x} \right| \tag{wzg. zmiada danych TU} \\
\left| \frac{f(x) - f(x + h)}{f(x)} \right| &\approx \tag{wzg. zmiana wyniku TU}\\
\left| \frac{f(x) - (f(x)+hf'(x))}{f(x)} \right| &= \\
\left| \frac{hf'(x)}{f(x)} \right| \left| \frac{x}{x} \right| &= \\
\left| \frac{x \cdot f'(x)}{f(x)} \right| \cdot \left| \frac{h}{x} \right|
\end{align*}
$$
Wielkość $\left| \frac{x \cdot f'(x)}{f(x)} \right|$ jest miarą *uwarunkowania* zadania obliczania wartości *ustalonej funkcji*.  
Jest to *wskaźnik uwarunkowania*.

### Przykład – Badanie Uwarunkowania Iloczynu Skalarnego

Obliczmy *uwarunkowanie* zadania wyznaczania iloczynu skalarnego dwóch wektorów.
$$
\begin{align*}
x = \begin{bmatrix} x_{1}, x_{2}, \dots, x_{n} \end{bmatrix}^{T} &\rightsquigarrow \widetilde{x} = \begin{bmatrix} x_{1}(1 + \epsilon_{1}), x_{2}(1 + \epsilon_{2}), \dots, x_{n}(1 + \epsilon_{n}) \end{bmatrix}^{T}\\
y = \begin{bmatrix} y_{1}, y_{2}, \dots, y_{n} \end{bmatrix}^{T} &\rightsquigarrow \widetilde{y} = \begin{bmatrix} y_{1}(1 + \alpha_{1}), y_{2}(1 + \alpha_{2}), \dots, y_{n}(1 + \alpha_{n}) \end{bmatrix}^{T} \\
S(x,y) = \sum\limits_{i=1}^{n}{x_{i}y_{i}} &\rightsquigarrow S(\widetilde{x},\widetilde{y}) = \sum\limits_{i=1}^{n}{x_{i}(1+\epsilon_{i})y_{i}(1+\alpha_{i})} = \sum\limits_{i=1}^{n}{x_{i}y_{i}(1+\epsilon_{i} + \alpha_{i} + \epsilon_{i}\alpha_{i})}
\end{align*}
$$
Teraz policzmy wskaźnik uwarunkowania:
$$
\begin{align*}
\left| \frac{S(x,y) - S(\widetilde{x},\widetilde{y})}{S(x,y)} \right| &= 
\left| \frac{\sum\limits_{i=1}^{n}{x_{i}y_{i}(\epsilon_{i} + \alpha_{i} + \epsilon_{i}\alpha_{i})}}{\sum\limits_{i=1}^{n}{x_{i}y_{i}}} \right| \\ &\approx
\left| \frac{\sum\limits_{i=1}^{n}{x_{i}y_{i}(\epsilon_{i} + \alpha_{i})}}{\sum\limits_{i=1}^{n}{x_{i}y_{i}}} \right| \\
&\le \underset{1 \le i \le n}{max}(|\epsilon_{i}| + |\alpha_{i}|) \cdot \frac{\sum\limits_{i=1}^{n}{|x_{i}y_{i}|}}{\left| \sum\limits_{i=1}^{n}{x_{i}y_{i}} \right|} \\
k(x,y) &= \frac{\sum\limits_{i=1}^{n}{|x_{i}y_{i}|}}{\left| \sum\limits_{i=1}^{n}{x_{i}y_{i}} \right|}
\end{align*}
$$

**Wnioski:** 

1. Jeśli $|x_{i}y_{i}| > 0$ dla $i \le i \le n$, to $k(x,y) = 1$, więc zadanie jest dobrze uwarunkowane
2. Zauważmy jednak, że $k(x,y)$ może być dowolnie duże:
   np. $\sum\limits_{i}|x_{i}y_{i}| = 1$, ale już $\sum\limits_{i}x_{i}y_{i}=10^{-100}$ 