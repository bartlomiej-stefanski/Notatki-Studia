Zasada indukcji dla liczb naturalnych:
Jeśli dla własności $P$ zachodzi $P(0)$ oraz $\forall{n \in \mathbb{N}} P(n) \implies P(n+1)$, to $\forall{n \in \mathbb{N}} P(n)$.

---
## Przykład

Zdefiniujmy funkcję `sumto` jako:
```ocaml
let rec sumto = function
| 0 -> 0
| n -> n + sumto (n - 1)
```

Pokażmy, że $P(n) : sumto(n) = \frac{n(n+1)}{2}$ zachodzi dla każdej liczby naturalnej $n$.

1. Podstawa indukcji trywialnie zachodzi: $sumto(0) = 0$
2. Załóżmy, że dla pewnego $n$ zachodzi $sumto(n) = \frac{n(n+1)}{2}$;
   Pokażmy, że $sumto(n+1) = \frac{(n+1)(n + 1 + 1)}{2}$:
$$
   \begin{equation} \begin{split}
   L =sumto(n + 1) \overset{def}{=} & \\
   (n + 1) + sumto(n + 1 - 1) = & \\
   (n + 1) + sumto(n) \overset{ind}{=} & \\
   (n + 1) + \frac{n(n + 1)}{2} = & \\
   \frac{n(n+1) + 2(n+1)}{2} = & \\
   \frac{(n + 1 + 1)(n+1)}{2} = R
   \end{split} \end{equation}
$$
Więc na mocy zasady indukcji $\forall{n \in \mathbb{N}} P(n)$.