**Dane:**
[[Gramatyki Bezkontekstowe|Gramatyka Bezkontekstowa]] $G$ oraz słowo $s$.

**Zadanie:**
Sprawdzić, czy $s$ jest elementem alfabetu $G$.

#### Gramatyka w Postaci Chomsky'ego

Jeżeli każda produkcja gramatyki bezkontekstowej $G$ jest postaci:

- $A \to BC$
- $A\to a$

Gdzie $A,B,C$ to symbole nieterminalne, a $a$ jest symbolem terminalnym, to $G$ jest w postaci normalnej Chomsky'ego.

#### Język Generowany Przez Gramatykę

Język $L(G)$ generowany przez gramatykę $G = (N,T,P,S)$ definiujemy jako:
$$
L(G) = \{w \mid w \in T^{*} \land S\overset{*}{\Rightarrow} w\}
$$
Gdzie $T^{*}$ jest zastosowaniem [[Języki Regularne#Gwiazdka Kleene'go|gwiazdki Kleen'ego]], a $\overset{*}{\Rightarrow}$ jest przechodnim domknięciem relacji wyprowadzalności z gramatyki.

## Algorytm Naiwny


Niech zbiór $F_{i}$ zawiera wszystkie słowa wyprowadzalne z gramatyki $G$. Początkowo $F_{0} = S$.
Następnie wykonamy $2|w| - 1$ następujących przejść:
$$
F_{i+1} = \bigcup_{w\in F_{i}}M(w)
$$
Gdzie $M(w)$ wyznacza wszystkie możliwe słowa wyprowadzalne przez zastosowanie co najwyżej jednej produkcji z $w$.

Wystarczą $2|w| - 1$ iteracje, bo dokładnie tyle potrzeba na utworzenie każdego słowa $|w|$ literowego.

#### Złożoność Obliczeniowa

Zależy głównie od liczności kolejnych $F_{i}$. Bardzo często jednak będzie wykładnicza, stąd potrzeba szybszego algorytmu.

## Programowanie Dynamiczne

Zauważmy, że jeśli $w = w_{1},w_{2},\dots,w_{n}$, to pierwszą użytą produkcją musi być $S\to AB$. Dalej rozwijanie produkcji $A,B$ przeprowadzane jest oddzielnie. Jakbyśmy wiedzieli jak podzielić ciąg liter $w$, to moglibyśmy otrzymać dwie instancje mniejszego problemu.

Ta obserwacja jest bardzo ważna, ale będziemy chcieli działać *od tyłu*: jeżeli dla każdego możliwego podziału $w$ na dwie części wiemy jakie symbole nieterminalne pozwalają wyprowadzić ten pod-napis, to wystarczy sprawdzać możliwe podziały do czasu znalezienia takiego, że istnieje produkcja $S \to AB$ oraz lewy przedział jest wyprowadzalny z $A$, a prawy z $B$.

Z tej obserwacji budujemy następującą zasadę programowania dynamicznego:
$$
\begin{align*}
dp[i][j] &= \text{zbiór produkcji z których można wyprowadzić }w_{i}\dots w_{j} \\
dp[i][j] &= \begin{cases}
\{A \mid (A\to w_{i}) \in P\} &: i = j \\
\bigcup\limits_{k=i}^{j-1} dp[i][k] \otimes dp[k+1][j] &: 1 \le i < j \le n
\end{cases}
\end{align*}
$$
Gdzie operator $\otimes$ definiujemy następująco:
$$
x \otimes y = \{A \mid (a \to BC)\in P \land B\in x \land C\in y\}
$$
> Intuicyjnie $x\otimes y$ wyznacza wszystkie zbiór wszystkich takich produkcji, z których można uzyskać nieterminały zawarte zarówno w $x$ i $y$.

### Złożoność Obliczeniowa

Algorytm wykonuje $\Theta(n^{3})$ operacji $\otimes$.
Operację $\otimes$ można napisać tak, by działała w czasie $O(|P|)$ lub $O(|N|^{2})$. Który sposób wybieramy powinien zależeć od naszych danych.