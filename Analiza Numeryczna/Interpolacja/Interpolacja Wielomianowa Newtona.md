
Będziemy chcieli znaleźć *postać Newtona* wielomianu interpolacyjnego:
$$
\begin{align*}
L_{n}(x) &= b_{0}p_{0}(x) + b_{1}p_{1}(x) + b_{2}p_{2}(x) + \dots + b_{n}p_{n}(x)\\
p_{n}(x) &= (x-x_{0})(x-x_{1})\dots(x-x_{n-1})
\end{align*}
$$
Teraz chcemy tak dobrać współczynniki $b_{0},b_{1},\dots,b_{n}$, że $L_{n}(x_{k}) = y_{k}$.

Mamy tyle samo niewiadomych co warunków, więc konstruujemy układ równań:
$$
\begin{align*}
L_{n}(x_{0}) &= b_{0} &&= y_{0}\\
L_{n}(x_{1}) &= b_{0} + b_{1}(x_{1}-x_{0}) &&=y_1\\
L_{n}(x_{2}) &= b_{0} + b_{1}(x_{2}-x_{0}) + b_{2}(x_{2}-x_{0})(x_{2}-x_{1}) &&= y_{2}\\
\vdots\\
L_{n}(x_{n}) &= b_{0}+b_{1}(x_{n}-x_{0}) + \dots + b_{n}(x_{n}-x_{0})\dots(x_n-x_{n-1}) &&= y_{n}
\end{align*}
$$
Układ można rozwiązać i wtedy otrzymamy *jawny* wzór na kolejne współczynniki:
$$
\tag{1}b_{k}=\sum\limits_{j=n}^{k}\frac{y_{j}}{\prod\limits_{i=0}^{k} x_{j}-x_{i}} = f[x_{0},x_{1},\dots,x_{k}]
$$
Do takiego wzoru można w czasie liniowym dodać *kolejną obserwację* – poprawa przybliżenia poprzez dodanie jednego pomiaru jest liniowa.

### Lepszy Wzór

Ze względów numerycznych nie zaleca się korzystania ze wzoru $(1)$ bezpośrednio. Lepsze efekty uzyska się korzystając z *ilorazu różnicowego*.

![[Iloraz Różnicowy#Definicja]]

---

#### Twierdzenie

$$
b_{k}=f[x_{0},x_{1},\dots,x_{k}]
$$
Do pokazania w domu.

#### Wniosek

Otrzymujemy nowy – lepszy wzór na obliczanie przybliżenia w postaci Newtona:

$$
\begin{align*}
L_{n}(x) &= \sum\limits_{k=0}^{n} f[x_0,\dots,x_{k}]p_{k}(x)\\
&\begin{cases}
p_{0}(x) = 1\\
p_{k}(x) = \prod\limits_{i=0}^{k-1} (x_{i}-x_{k})
\end{cases}
\end{align*}
$$

### Tablica Ilorazów Różnicowych

Zauważmy, że jeśli dodamy nową obserwację, to uaktualniony wzór będzie postaci:
$$
L_{n+1} = L(n) + b_{n+1}p_{n+1}(x)
$$
![[Iloraz Różnicowy#Wyznaczanie Ilorazów Różnicowych]]

> **Zadanie domowe:** jak pamiętając tylko przekątną tablicy ilorazów różnicowych wyznaczyć następną wartość w czasie liniowym?

#### Zalety Postaci Newtona Wielomianu Interpolacyjnego

1. Łatwo dodajemy kolejne obserwacje – niemożliwe przy postaci Lagrange'a
2. Zakładając, że obliczyliśmy już współczynniki postaci Newtona $b_{0},b_1,\dots,b_{n}$, (koszt $O(n)$), to wartość $L_{n}(x)$, gdzie $x$ jest dany obliczymy stosując uogólniony schemat Hornera w czasie $O(n)$ – postać Lagrange'a liczymy w $O(n^{2})$

#### Algorytm Niepoprawny Numerycznie

Metoda wypełniania tablicy z ilorazami różnicowymi jest algorytmem niepoprawnym numerycznie – dokładność traci już dla około $30$ wyrażeń.

By ograniczyć występowanie błędów można:

- Posortować węzły
- Algorytm wyznaczania ilorazów różnicowych na podstawie podanej zależności rekurencyjnej *nie jest* algorytmem numer
