> Wykorzystanie definicji do udowodnienia lematów o funkcjach.

## Przykład 1

Dla funkcji zdefiniowanych jako:
```ocaml
let compose f h x = f (g x);;
let twice f x = f (f x);;
```

 Pokazać, że dla dowolnej funkcji `h: a -> a` zachodzi `twice h x == compose h h x`:
```
twice h x = (z def. twice)
h (h x) = (z def. compose)
compose h h x
```

---

## Przykład 2

Zdefiniujmy złożenie funkcji jako:
```ocaml
let (<<) = compose;
```

Pokazać, że dla każdego `f`, `g`, `h` i `x` zachodzi `((f << g) << h) x == (f << (g << h)) x`:
```
((f << g) << h) x = (z def. <<)
(f << g) (h x) = (z def. <<)
f (g (h x)) = (z def. <<)
f ((g << h) x) = (z def. <<)
(f << (g << h)) x
```