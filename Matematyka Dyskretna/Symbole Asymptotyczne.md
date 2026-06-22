---
tags:
  - MDM-checklist
---
## Duże O

Intuicyjnie funkcja $f$ rośnie *co najwyżej* tak samo szybko jak $g$.
$$f(n) = O(g(n)) \iff \exists_{c>0}\ f(n) \le cg(n) \text{ dla prawie wszystkich n}$$

## Omega

Intuicyjnie funkcja $f$ rośnie *co najmniej* tak samo szybko jak $g$. 
$$f(n) = \Omega(g(n)) \iff \exists_{c>0}\ f(n) \ge cg(n)$$

## Małe O

Intuicyjnie funkcja $f$ rośnie *wolniej* niż funkcja $g$.
$$f(n) = o(g(n)) \iff \lim_{n \rightarrow \inf} {\frac{f(n)}{g(n)}} =   0$$
Symbol ten pozwala również na zdefiniowanie relacji *asymptotycznie rośnie wolniej* pomiędzy dwoma funkcjami: 
$$f(n) = o(g(n)) \iff f(n) \prec g(n)$$

## Theta

Intuicyjnie funkcja $f$ rośnie tak samo szybko jak $g$ z dokładnością do pewnej stałej.
$$f(n) = \Theta(g(n)) \iff \exists_{e,d>0}\ cg(n) \le f(n) \le dg(n)$$

### Funkcje asymptotyczne

Jest to warunek *silniejszy* niż $\Theta$, bo wymaga on *dokładnie takiego samego* tępa wzrostu.
$$f(n)\ \sim\ g(n) \iff \lim_{n \rightarrow \inf}\frac{f(n)}{g(n)} = 1$$