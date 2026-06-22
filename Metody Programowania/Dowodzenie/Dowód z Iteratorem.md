> Jeśli funkcja ma w sobie jakiś [[Iterators|iterator]], to może być łatwiej zacząć od jakiegoś lematu;
> Reszta wygląda właściwie bardzo podobnie do [[Dowód z Indukcją]].
## Przykład

Zdefiniujmy dwie funkcje do obliczania silni:
```ocaml
let rec fact n =
	if n = 0 then 1 else n * fact (n - 1)

let iter_fact n =
	let it_fact n acc = 
		if n = 0 then acc
		else it (n-1) (acc * n)
	in it_fact n 1;;
```

Pokażmy, że dla $\forall_{n \in \mathbb{N}} fact(n) = iter\_fact(n)$.

Zaczniemy od pokazania **lematu**, że dla każdego $n$ zachodzi $it\_fact(n,acc) = acc * fact(n)$:
1. Podstawa indukcji:$$fact\_it(0,acc)\overset{def}{=}acc=acc * 1 = acc * fact(0)$$
2. Załóżmy, że lemat jest spełniony dla pewnego $n$, pokażmy dla $(n+1)$:
   $$\begin{equation} \begin{split}
   fact\_it(n+1,acc)\overset{def}{=} & \\
   fact\_it(n,acc\cdot(n+1))\overset{ind}{=} & \\
   acc\cdot(n+1) * fact(n)\overset{def}{=} & \\
   acc * fact(n+1)_{\square}
\end{split}\end{equation}$$
**Lemat** zachodzi więc dla każdego $n \in \mathbb{N}$.

Wróćmy teraz do zasadniczego twierdzenia i pokażmy je używając lematu:
$$\begin{equation} \begin{split}
iter\_fact(n)\overset{def}{=} & \\
fact\_it(n,1)\overset{lemat}{=} & \\
1 * fact(n) = & \\ fact(n)_{\square}
\end{split}\end{equation}$$
