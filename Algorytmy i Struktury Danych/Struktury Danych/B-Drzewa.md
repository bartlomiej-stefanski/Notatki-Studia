Co jeżeli chcemy zaimplementować strukturę słownikową, ale pracujemy z ogromnym zbiorem danych, który nie zmieści się w pamięci operacyjnej?

W takim przypadku najbardziej będzie nam zależało na minimalizacji liczby operacji dyskowych, bo będą one znacząco wolniejsze od przetwarzania tych danych (o rzędy wielkości).

Problem ten rozwiązują B-drzewa, których główne cechy charakterystyczne to:

- Wszystkie wierzchołki leża na tej samej głębokości
- Każdy węzeł zawiera wiele elementów zbioru (w kolejności – prawdopodobnie tablica wskaźników/linked list)
- Zwiększanie wysokości jest ściśle minimalizowane

## Definicja

Struktura jest B-drzewem jeżeli:

1. Każdy węzeł $x$ przechowuje następujące informacje:
	- `n` – liczba kluczy pamiętanych w $x$.
	- `2t - 1` pól $key[]$ przeznaczonych na klucze pamiętane w kolejności porządku.
	- `leaf` – pole logiczne wyznaczające, czy wierzchołek jest drzewem.
		- Jeżeli nie jest liściem, to `2t` pól $c[]$ przechowujących wskaźniki na dzieci.
2. Klucze pamiętane w poddrzewie o korzeniu $c[x]$ są nie mniejsze od kluczy pamiętanych w poddrzewie o korzeniu $c[j], j < x$ i nie większe od tych w $c[k],k>x$.
3. Wszystkie liście mają tą samą głębokość $h$.
4. $t \ge 2$ jest ustaloną liczbą całkowitą określającą dolną i górną granicę na liczbę kluczy pamiętanych w węzłach:
	- Każdy węzeł różny od korzenia musi pamiętać co najmniej $t-1$ kluczy (a więc musi mieć co najmniej $t$ dzieci). Jeśli drzewo jest niepuste, to korzeń musi pamiętać co najmniej jeden klucz.
	- Każdy węzeł może pamiętać co najwyżej $2t-1$ kluczy (a więc może mieć co najwyżej $2t$ dzieci). Jeżeli węzeł zawiera dokładnie $2t-1$ to nazywamy go *pełnym*.

> Na efektywniejszą implementację struktury pozwala *globalne* przechowywanie wszelkich tablic i danych związanych z wierzchołkami.

## Operacje Na Drzewie

> **UWAGA:** w implementacji prawdopodobnie jest sporo błędów off-by-one dla indeksów.

Zakładamy, że dane są dostępne jedynie gdy załadujemy je z dysku funkcją `disc_read(data)`. Podobnie do zapisu musi zostać wydane polecenie `disc_write(data)` dla wcześniej załadowanych danych.
Dodatkowo zakładamy, że dane załadowane do pamięci można *normalnie* modyfikować, a nie używane dane zostaną *automatycznie* zastąpione innymi.

> Naszym celem jest minimalizacja wywołań `disc_*`, bo uznajemy je za bardzo wolne (w rzeczywistości tak faktycznie jest).

### Find

Wykonywane jak dla zwykłych drzew binarnych tylko tym razem mamy do wykonania dodatkowe wyszukiwanie wewnątrz wierzchołka:
```python
def btree_search(node, k):
	disc_read(node)
	x = lower_bound(node.key, k)
	if node.key == x:
		return c[x] # Ktoś będzie musiał wykonać na tym disc_read
	else:
		btree_search(c[x], k)
		# Albo tail-recursive jump jak już jesteśmy tak low-level...
```

> W zależności od wielkości $t$ możemy chcieć, by `lower_bound` było liniowym przeszukaniem lub binary search.

### Create

Tworzenie nowego node wymaga operacji dyskowej i właściwie tylko dlatego ta operacja dostała swoją własną sekcję...
```python
def btree_create():
	node = disc_alloc(sizeof(btree_node))
	node.n = 0
	node.leaf = true
	disc_write(node)
	return node
```

### Insert

Właściwa insercja wydarzy się dopiero w funkcji pomocniczej – tutaj sprawdzimy czy dodanie kolejnej wartości nie przepełniło by wierzchołka, a jeśli tak, to rozdzielamy go przed rozpoczęciem dodawania:

```python
def btree_insert(root, k):
	disc_read(root)
	if root.n == 2t - 1:
		s = btree_create()
		s.leaf = false
		s.n = 1
		s.c[1] = root
		btree_split_child(s, 1)
		btree_insert_nonfull(s, k)
	else:
		# wszystko ok -> można wstawiać
		btree_insert_nonfull(root, k)
	
```

#### Rozdzielanie Węzła

Jeżeli pewien wierzchołek (nie będący korzeniem) jest pełny i chcemy wykonać do niego wstawienie, to należy rozdzielić go na dwie części. Funkcja przyjmuje wskaźnik na rodzica pełnego wierzchołka oraz indeks pod którym jest zawarty w tablicy `c` wskaźników  na dzieci.
```python
def btree_split_child(parent, i):
	new_node = btree_create()
	full_node = parent.c[i]
	
	new_node.leaf = full_node.leaf
	new_node.n = t - 1
	full_node = t - 1
	
	# Zakresy podawane włącznie.
	for j in 1..(t-1):
		new_node.key[j] = full.key[j + t]
	if not full_node.leaf:
		for j in 1..(t-1):
			new_node.c[j] = full.c[j + t]
	
	# Shift right kluczy i wskaźników ojca by zrobić miejsce na new_node
	for j in (parent.n)..(i+1):
		p.c[j+1] = p.c[j]
		p.key[j] = p.key[j-1]
	
	parent.c[i+1] = new_node
	parent.key[i] = full_node.key[t] # Zabieramy ostatni z full_node
	parent.n += 1
	
	disc_write(parent)
	disc_write(new_node)
	disc_write(full_node)
```

#### Wstawianie z Niepełnym Korzeniem

Procedura ta przejdzie ścieżkę od korzenia do odpowiedniego liścia, rozdzielając wszystkie pełne wierzchołki po drodze. Kluczowe jest, by parametr `root` nie był pełnym wierzchołkiem.
```python
def btree_insert_nonfull(parent, k):
	disc_read(parent)
	inx = lower_bound(parent.key, k)
	if parent.leaf:
		for j in parent.n..(inx):
			parent.key[j+1] = parent.key[j]
		
		parent.key[inx] = k
		parent.n += 1
		disc_write(parent)
	else:
		disc_read(parent.c[inx])
		candidate = parent.c[inx]
		if candidate.n == 2t - 1:
			btree_split_child(parent, inx)
			# Prawa część candidate jest teraz osobnym wierzchołkiem.
			# Trzeba sprawdzić, czy być możę chcieliśmy tam iść.
			if k > parent.key[inx]:
				inx += 1
				candidate = parent.c[inx]
		
		btree_insert_nonfull(candidate, k)
```

### Delete

Operacja *wysoko poziomowo* przechodzi podobnie do [[Drzewa AVL#Usuwanie|AVL-delete]], ale nisko-poziomowo wymaganych jest wiele korekt uwzględniających wewnętrzną strukturę AVL.

Implementację przeprowadzimy podobnie do insert – będziemy mieć specjalny przypadek dla korzenia i dodatkową funkcję oczekującą wierzchołków tym razem *pełniejszych* niż $t-1$. 
```python
def btree_delete(root, k):
	if root.n == 1 && root.key[1] == k:
		# Korzeń ma tylko dwóch synów i musimy z któregoś zabrać element
		(l, r) = (root.c[1], root.c[2])
		disc_read(l) disc_read(r)
		
		if l.n >= t:
			root.key[1] = btree_find_largest(l)
			btree_delete_nonempty(l, root.key[1])
		else if r.n >= t:
			root.key[1] = btree_find_smallest_and_delete(r)
			btree_delete_nonempty(r, parent.key[1])
		else:
			# Oba mniejsze niż t? -> można połączyć! -> zmniejszamy wysokość
			root = btree_merge(l, r)
		
		disc_write(root)
	else:
		btree_delete_nonempty(root, k)
```

#### Merge

Funkcja łączy dwa wierzchołki o $t-1$ kluczach w jeden:
```python
def btree_merge(l, r):
	# Dopisujemy dodatkowe elementy do l
	for i in 1..t:
		l.key[t + i - 1] = r.key[i] # nie ma ostatniego, ale trudno
		l.c[t + i] = r.c[i]
	
	l.n = 2t - 1
	disc_write(l)
	disc_dealloc????(r)
```

#### Delete Na Niepustych Drzewach

```python
def btree_delete_nonempty(parent, k):
	inx = lower_boun(parent.key, k)
	
	if parent.key[inx] == k:
		# Wierzchołek do usunięcia
		if parent.leaf:
			"przszesuń klucze z przedziału [inx+1, parent.n] w lewo"
			# Powyższa operacja przesłoni klucz inx
			parent.n -= 1
			disc_write(parent)
		else:
			(l, r) = (parent.c[inx], parent.c[inx+1])
			disc_read(l) disc_read(r)
			if l.n >= t:
				parent.key[inx] = btree_find_largest(l)
				btree_delete_nonempty(l, parent.key[inx])
			else if r.n >= t:
				root.key[1] = btree_find_smallest(r)
				btree_delete_nonempty(r, parent.key[1])
			else:
				# Nie ma z kogo kraść elementów -> trzeba połączyć
				parent.c[inx] = btree_merge(l, r)
				"przszesuń klucze z przedziału [inx+1, parent.n] w lewo"
				# Powyższa operacja przesłoni klucz inx
				disc_write(parent)
	else:
		# Wierzchołek do usuwania jest gdzieś niżej
		candidate = parent.c[inx]
		disc_read(candidate)
		if candidate.n >= t:
			btree_delete_nonempty(candidate, k)
		else if inx > 1:
			# Istnieje coś na lewo
			l = parent.c[inx-1]
			disc_read(l)
			if l.n >= t:
				"przesuń klucze parent o 1 w prawo"
				parent.key[1] = l.key[l.n]
				parent.c[1] = l.c[l.n+1]
				l.n -= 1
				parent.n += 1
				disc_write(l) disc_write(parent)
				btree_delete_nonempty(candidate, k)
		else if inx < n:
			# Podobnie co z lewej strony, tylko że w prawo...
			...
```

#### Find Largest/Smallest

Funkcje rekurencyjnie zejdą do liści drzewa, by naleźć odpowiednio najmniejszy/największy element.
```python
def btree_find_largest(node):
	disc_read(node)
	if node.leaf:
		return node.key[node.n]
	
	return btree_find_largest(node.c[node.n+1])
```
Znajdywanie elementu najmniejszego odbywa się izomorficznie.

### Złożoność Operacji

**Twierdzenie:**
Dla $n\ge 1, t\ge 2$ dla każdego B-drzewa jego wysokość to co najwyżej $\log_{t} \frac{n+1}{2}$
**d-d:**
Każdy poziom (oprócz korzenia) posiada co najmniej $t$ synów – stąd $\log_{t}$. Dzielenie przez $2$ pochodzi z przechowywania danych nie tylko w liściach.

Wnioskujemy z tego twierdzenia, że $h = \Theta(\log_{t} n)$, co daje nam następujące oszacowania na koszty poszczególnych operacji:


| Procedura             | Liczba Operacji Dyskowych | Koszt Pozostałych Operacji |
| --------------------- | ------------------------- | -------------------------- |
| Search                | $O(h)$                    | $O(th)$                    |
| Create                | $O(1)$                    | $O(1)$                     |
| Split Child           | $O(1)$                    | $O(t)$                     |
| Insert                | $O(h)$                    | $O(th)$                    |
| Merge                 | $O(1)$                    | $O(1)$                     |
| Find Largest/Smallest | $O(h)$                    | $O(h)$                     |
| Delete                | $O(h)$                    | $O(th)$                    |
