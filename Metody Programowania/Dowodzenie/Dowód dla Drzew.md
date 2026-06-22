> Będzie to po prostu [[Dowód z Indukcją|dowód indukcyjny]] przeprowadzony dla drzew.

```ocaml
type 'a tree = Leaf | Node of 'a tree * 'a * 'a tree
```

Zasada Indukcji dla drzew, dla każdej własności `P`. Jeśli:

1. `P(Leaf)`
2. Oraz dla każdego `a : 'a` i `l,r : 'a tree`, `P(l)` i `P(r)` implikuje `P(Node(l, a, r))`

To dla każdego drzewa `t` zachodzi własność `P(t)`.

---
## Przykład

```ocaml
let rec reflect = function
| Leaf -> Leaf
| Node (l, v, r) -> Node (reflect r, v, reflectr l)
```

Pokażmy teraz, że `reflect (reflect) t = t`. Skorzystajmy z zasady indukcji dla drzew.

1. Dla `Leaf` twierdzenie jest trywialnie spełnione:
```
reflrect (reflect Leaf) = (z def.)
reflect Leaf = (z def.)
Leaf
```

2. Weźmy dowolne `l`, `r` i `v`. Załóżmy, że `reflect (reflect l) = l` i `reflect (reflect r) = r`. 
   Pokażmy teraz, że `reflect (reflect Node(l, v, r)) = Node(l, v, r)`:
```
reflect (reflect Node(l, v, r)) = (z def.)
reflect (Node(reflect r, v, reflect l)) = (z def.)
Node(reflect (reflect l), v, reflect (reflect r)) = (z ind.)
Node(l, v, r)
```
Na mocy zasady indukcji dla każdego drzewa `t` zachodzi `reflect (reflect t) = t`.
