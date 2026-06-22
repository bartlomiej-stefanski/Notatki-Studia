```ocaml
type 'a list = [] | (::) of 'a * 'a list;;
```

Zasada indukcji dla typu `list`, dla każdej własności $P$:
Jeśli zachodzi:

1. $P([])$
2. Dla każdego `a : 'a` i `as : 'a list` zachodzi implikacja $P(as) \implies P(a :: as)$

To własność $P$ jest spełniona dla każdej listy.

---

## Przykład 1

Pokażmy, że dla każdej listy `as` zachodzi `append [] as`:
```
append [] as = (z def. append)
as
```

Pokażmy [[Dowód z Indukcją|indukcyjnie]], że dla każdej listy `as` zachodzi `append as []`:

1. `append [] [] = []`
2. Weźmy dowolne `as`, załóżmy że zachodzi `append as []`, pokażmy że dla każdego `a` zachodzi `append (a :: as) [] = a :: as`:

```
append (a :: as) [] = (z def. append)
a :: append as [] = (z zał. ind.)
a :: as
```

---
## Przykład 2

```ocaml
let (@) = append;;
```

Pokażmy, że dla każdego `xs`, `ys`, i `zs` zachodzi `(xs @ ys) @ zs = xs @ (ys @ zs)`.
Będzie to dowód indukcyjny względem `xs`:

1. Pokażmy, że dla `xs = []` i każdego `ys` i `zs` zachodzi
   `([] @ ys) @ zs = [] @ (ys @ zs)`:

```
([] @ xs) @ ys = (z def. @)
xs @ ys = (z def. @)
[] @ (xs @ ys)
```

2. Weźmy dowolne `xs`. Załóżmy, że dla każdego `ys`, `zs` zachodzi teza.
   Pokażmy teraz, że zachodzi `((x :: xs) @ ys) @ zs = (x :: xs) @ (ys @ zs)`:

```
((x :: xs) @ ys) @ zs = (z def. @)
(x :: (xs @ ys)) @ zs = (z def. @)
x :: ((xs @ ys) @ zs) = (z zał. ind.)
x :: (xs @ (ys @ zs)) = (z def. @)
(x :: xs) @ (ys @ zs)
```

---

## Przykład 3

```ocaml
let rec rev = function
| [] -> []
| x :: xs -> rev xs @ [x]

let itRev xs =
	let rec revapp xs ys = match xs with
	| [] -> ys
	| x :: xs' -> revapp xs' (x :: ys)
	in revapp xs [];;
```

Pokażmy teraz, że dla każdej listy `xs` zachodzi `rev xs = itRev xs`.

Do dowodu potrzebować będziemy udowodnić **lemat**: $\forall_{ys}\ rev(xs) @ ys = revapp(xs, ys)$  
Pokażemy to indukcją:

1. Dla każdego `ys` zachodzi $rev([], ys) = revapp([], ys)$:
$$\begin{equation} \begin{split}
rev([]) @ ys\overset{def\ rev}{=} & \\
[] @ ys \overset{def\ @}{=} & \\
ys \overset{def\ revapp}{=} & \\
revapp([], ys)
\end{split}\end{equation}$$
2. Weźmy dowolny `xs`. Pokażę, że jeśli dla każdego `ys` zachodzi $rev(xs) @ ys = revapp(xs, ys)$, to również $rev(x::xs) @ ys = revapp((x :: xs), ys)$:
$$\begin{equation} \begin{split}
rev(x::xs)@ys \overset{def\ rev}{=} & \\
(rev(xs) @ [x]) @ ys \overset{łączność @}{=} & \\
rev(xs) @ ([x] @ ys) \overset{ind}{=} & \\
revapp(xs, [x] @ ys) \overset{def\ op.}{=} & \\
revapp(xs, x :: y) \overset{def\ revapp}{=} & \\
revapp(x :: xs, y)
\end{split}\end{equation}$$

Teraz możemy już wrócić do właściwego twierdzenia - `rev xs = itRev xs`:
```
itRev xs = (z def.)
revapp xs [] = (z lematu)
rev xs @ [] = (z wcześniejszgo dowodu)
rev xs
```
Co kończy dowód.