---
tags:
  - MDM-checklist
---
**Definicja:** $\mathbb{Z}_{n}^{*} = \{x\in\mathbb{Z}_{n} | \exists x^{-1}\} = \{x\in\mathbb{Z}_{n}| x\bot n\}$

**Funkcja Eulera:** $\phi(n) = |\mathbb{Z}_{n}^{*}|$

## Obserwacje

- $p\in\mathbb{P} \implies \phi(p) = p-1$
- $p\in\mathbb{P}\implies \phi(p^{\alpha}) = p^{\alpha} -p^{\alpha-1}$
- $m_{1}\bot m_{2} \implies \phi(m_{1}m_{2}) = \phi(m_{1})\phi(m_{2})$
- $\phi(n) = \phi(p_{1}^{\alpha_{1}}\dots p_{k}^{\alpha_{k}}) = p_{1}^{\alpha_{1}}\dots p_{k}^{\alpha_{k}}\left(1-\frac{1}{p_{1}}\right)\dots\left(1-\frac{1}{p_{k}}\right)= n\left(1-\frac{1}{p_{1}}\right)\dots\left(1-\frac{1}{p_{k}}\right)$

## Twierdzenie Eulera

Jeśli $a\bot n$ to $a^{\phi(n)} \equiv 1 \mod n$ oraz  $n | a^{\phi(n)} - 1$

**d-d:** dla $a\bot n$
$$
\begin{align*}
\prod_{x\in\mathbb{Z}_{n}^{*}}x= \prod_{x\in\mathbb{Z}_{n}^{*}} a x
\end{align*}
$$
Dlaczego? Zauważmy, że po obu stronach znajduje się tyle samo czynników oraz wszystkie są względnie pierwsze z $n$. (bo iloczyn względnie pierwszych elementów też jest względnie pierwszy). Nie powtarzają się przez względną-pierwszość z $n$.

Stąd otrzymujemy następujące równanie po modulo:
$$
\begin{align*}
\left(\prod_{x\in\mathbb{Z}_{n}^{*}}x\right)\mod n = \left(\prod_{x\in\mathbb{Z}_{n}^{*}} a x\right) \mod n = \left(a^{|\mathbb{Z}_{n}^{*}|}\cdot\prod_{x\in\mathbb{Z}_{n}^{*}} x\right) \mod n
\end{align*}
$$
Z tego dalej możemy wyciągnąć bardziej przydatne wnioski:
$$
\begin{align*}
1\mod n &= a^{|\mathbb{Z}_{n}^{*}|}\mod n\\
1&\equiv a^{|\mathbb{Z}_{n}^{*}|}\mod n\\
1&\equiv a^{\phi(n)} \mod  n
\end{align*}
$$

> Wniosek: $a^{-1} \equiv a^{\phi(n) - 1} \mod n$

### Małe Twierdzenie Fermata

$$
\begin{align*}
p\in\mathbb{P} \land \neg(p|a) \implies& \\
&a^{p-1}\equiv 1\mod p\\
&a^{p}\equiv a\mod p
\end{align*}
$$
Bezpośredni wniosek z twierdzenia Eulera.