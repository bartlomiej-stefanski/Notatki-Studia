**Dane:**
Ciąg $A = (a_{1},a_{2},\dots)$ oraz ciąg $B = (b_{1},b_{2},\dots)$.

**Zadanie:**
Jaki najdłuższy ciąg $C=(c_{1},c_{2},\dots)$ taki, że $C$ jest podciągiem $A$ oraz $B$.

Oznaczmy zbiór wszystkich najdłuższych podciągów jako $LCS(A,B)$.

## Programowanie Dynamiczne

**Obserwacja:**

- Jeżeli $a_{n}=b_{m}$, to ta litera kończy każdy ciąg z $LCS(A,B)$
- Jeżeli $a_{n}\ne b_{m}$, to istnieje ciąg w $LCS$ który nie kończy się na $a_{n}$ lub na $b_{m}$.

Prowadzi nas to do następującego wzoru:
$$
\begin{align*}
dp_{i,j} &= \begin{cases}
0 : i=0\lor j=0\\
d_{i-1,j-1} + 1: a_{i} = b_{j}\\
\max(d_{i,j-1}, d_{i-1,j}) : a_{i} \ne b_{j}
\end{cases}
\end{align*}
$$

### Złożoność

#### Czasowa

Wyliczenie każdego pola tablicy $dp$ zajmuje stały koszt, ale tych elementów jest $nm$ stąd złożoność obliczeniowa to będzie $\Theta(nm)$.

#### Pamięciowa

*Standardowo* przechowywalibyśmy całą tablicę $dp$, co implikowało by złożoność $\Theta(nm)$, ale możemy zauważyć, że *następny* rząd/kolumna zależy jedynie od poprzedniej. Oznacza to, że wystarczy nam przechowywać dwa rzędy/kolumny co pozwala uzyskać złożoność pamięciową $\Theta(n + m)$.

### Przykład

$$
\begin{align*}
\begin{array}{c|c c c c c c}
d_{i,j} & \epsilon & B & A & R & A & N\\
\hline
\epsilon & 0 & 0 & 0 & 0 & 0 & 0\\
R & 0 & 0 & 0 & 1 & 1 & 1\\
A & 0 & 0 & 1 & 1 & 2 & 2\\
B & 0 & 1 & 1 & 1 & 2 & 2\\
A & 0 & 1 & 2 & 2 & 2 & 2\\
N & 0 & 1 & 2 & 2 & 2 & 3
\end{array}
\end{align*}
$$

### Odtwarzanie Podciągu

Jak teraz odtworzyć podciąg?
Zaczynamy od ostatniej kratki tablicy i po kolei:

- Jeżeli litery były równe to dodajemy je do pod-słowa i idziemy po przekątnej
- Jeżeli nie, to idziemy tam gdzie był max i nic nie dodajemy.

> Jak ograniczyć zużywaną pamięć będzie na ćwiczeniach (Algorytm Hikschberga).
> Patrzeć [[AISD Lista 4#Zadanie 4|AISD Lista 4, Zadanie 4]].
