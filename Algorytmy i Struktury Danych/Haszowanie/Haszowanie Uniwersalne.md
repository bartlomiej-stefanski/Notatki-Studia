Dla każdej funkcji haszującej istnieją *niefortunne* dane dla których czas operacji słownikowych będzie duży. Przykładowo możemy wybrać takie dane, że dla wszystkich kluczy dostajemy te same wartości – przy implementacji [[Haszowanie#Listy Elementów|listowej]] będzie to skutkowało czasem kwadratowym.

Stąd potrzebujemy ochronić się przed takimi sytuacjami i w tym celu podobnie jak przy [[Quicksort]] skorzystamy z randomizacji: na początku działania programu będziemy losować funkcję haszującą.

**Definicja 1:**
Rodzinę funkcji haszujących $H$ nazywamy *uniwersalną*, jeżeli:
$$
\forall_{x,y\in U; x\ne y} |\{h \in H : h(x) = h(y)\}| \le \frac{|H|}{m}
$$
Czyli intuicyjnie dla dowolnych dwóch elementów $x,y$ z Uniwersum, liczba funkcji haszujących $h\in H$ dla których występuje kolizja ma być *możliwie mała*.

**Wniosek z Definicji:**
Prawdopodobieństwo, że przy *losowo* wybranej funkcji haszującej z $H$ elementy $x,y$ kolidują wynosi $\frac{1}{m}$.

**Twierdzenie 3:**
Niech $H$ będzie uniwersalną rodziną funkcji haszujących. Dla dowolnego zbioru $n \le m$ kluczy, liczba kolizji w jakich bierze udział ustalony (dowolny) klucz $x$ jest w średnim przypadku mniejsza od $1$.
**d-d:**
Policzmy $C_{x} =$ w ilu kolizjach może maksymalnie uczestniczyć element $x$ na przestrzeni wszystkich funkcji haszujących:
$$
C_{x} \le \sum\limits_{y\ne x} \frac{|H|}{m} = (n-1) \frac{|H|}{m}
$$
Teraz jeżeli każdą funkcję haszującą wybieramy z równym prawdopodobieństwem $\frac{1}{|H|}$, to wartość oczekiwana $E(C_{x})$ jest nie większa niż $\frac{n-1}{m}$.

## Przykłady Rodzin Uniwersalnych

### R1

Niech $m$ będzie liczbą pierwszą oraz $|U| < m^{r+1}$. Dla każdego $0 \le a < m^{r+1}$ definiujemy funkcję haszującą:
$$
h_{a}(x) = \sum\limits_{i=0}^{r}a_{i}x_{i}\text{ mod } m
$$
gdzie sekwencje $\langle a_{0}, a_{1},\dots,a_{r}\rangle, \langle x_{0},x_{1},\dots,x_{r}\rangle$ odpowiadają reprezentacji liczb $a,x$ w systemie $m$-arnym.

**Twierdzenie 4:**
Rodzina funkcji w stylu $R_{1}$ jest uniwersalną rodziną haszującą.
**d-d:**
#TODO 

### R2

Niech $p$ będzie liczbą pierwszą większą niż uniwersum kluczy i niech $m$ będzie wielkością tablicy haszującej.

> $Z_{p}^{*} = \{1,2,\dots,p-1\}, Z_{p} = \{0,1,\dots,p-1\}$

Dla dowolnych $a\in Z_{p}^{*}$ i $b\in Z_{p}$ zdefiniujmy funkcję haszującą:
$$
h_{a,b}(x) = ((ax + b)\text{ mod } p) \text{ mod }m
$$
**Twierdzenie:**
Zbiór funkcji:
$$
H_{p,m} = \{h_{a,b} : a\in Z_{p}^{*} \land b \in Z_{p}\}
$$
jest rodziną uniwersalną.
**d-d:**
Niech $h_{a,b}'(x) = (ax + b)\text{ mod } p$ dla odpowiadającej funkcji $h_{a,b}$. Dalej niech $k,l$ będą różnymi kluczami i niech $s = h'(k), r = h'(l)$. 
Z tego mamy:
$$
r - s \equiv a(k - l) \text{ mod } p
$$
Dlatego, że $p$ jest pierwsze oraz $a$ i $k - l$ nie przystają do zera [[Arytmetyka Modulo|modulo]] $p$ otrzymujemy również, że ich iloczyn jest nie zerowy modulo $p$ co daje nam $r \ne s$.
Czyli po ludzku: wartości $k,l$ każda funkcja $h_{a,b}'$ odwzorowuje na różne $s,r$ modulo $p$.

Dalej pokażemy, że każda para $a,b$ odpowiada innemu mapowaniu różnych $k,l$ na różne $r,s$.
Zauważmy, że możliwych par $a,b$ (czyli również funkcji $h_{a,b}$) jest tyle samo co możliwych par $r,s$. Można pokazać, że istnieje bijekcja pozwalająca wyznaczyć $a,b$ na podstawie $k,l,r,s$:
$$
\begin{align*}
a &= ((r - s)((k - l)^{-1} \text{ mod }p)) \text{ mod }p \\
b &= (r - ak) \text{ mod }p
\end{align*}
$$
Oznacza to, że dokładnie jedna funkcja $h_{a,b}'$ przekształca $k,l$ na $r,s$.

Z tego otrzymujemy, że oczekiwana liczba kolizji kluczy $k, l$ równa jest oczekiwanej liczbie par różnych $s,r$ mniejszych niż $p$ przystających po modulo $m$.
Dla ustalonej liczby $s$ liczba $r$ przystających do $s$ modulo $m$ wynosi $\left\lfloor  \frac{p}{m}  \right\rfloor - 1 \le \frac{p + m - 1}{m} = \frac{p-1}{m}$.
Różncyh $t$ dla takiego wybranego $s$ jest dokładnie $p-1$, stąd prawdopodobieństwo, ze $s,t$ kolidują jest nie większe niż $\frac{1}{m}$.

