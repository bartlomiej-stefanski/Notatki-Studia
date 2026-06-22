**Dane:**
$s_{1},s_{2},\dots,s_{n}$ – słowa

**Zadanie:** 
Znaleźć słowo $s$ takie, że:

- $\forall_{i}s_{i}\text{ jest podsłowem słowa } s$
- $|s|$ – minimalne

> Ten problem jest NP trudny.

## Rozwiązanie Zachłanne

**Założenie:**
$\forall_{i,j}s_{i}\text{ nie jest podsłowem }s_{j}$.
To odrobinę ułatwi wyszukiwanie i niczego nie zepsuje – podsłowa będą zawarte w swoich super-słowach.

### Strategia Zachłanna

$S = \{s_{1},\dots,s_{n}\}$
Niech $s_{i}$ oraz $s_{j}$ będą słowami z $S$ o najdłuższej *nakładce* – nachodzą na siebie najbardziej ze wszystkich.

Niech $s'$ będzie słowem powstałym z połączenia $s_{i}$ oraz $s_{j}$.
Wtedy chcemy zmienić $S \leftarrow S\setminus \{s_{i}, s_{j}\} \cup \{s'\}$.
Powtarzamy algorytm dopóki $|s| \ne 1$.

> To będzie działać w czasie wielomianowym.

### Jak Dobre Rozwiązania Otrzymamy?

Nie więcej niż czterokrotnie dłuższe od optymalnego.
Dlaczego? Zadanie dla czytelnika. #TODO

## Redukcja Do [[Set Cover]]

#TODO 
