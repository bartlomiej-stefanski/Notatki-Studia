> Jest to gramatyka formalna, w której wszystkie reguły wyprowadzenia wyrażeń są postaci:
> $A \rightarrow \mathcal{R}$ 
> Gdzie $A$ jest dowolnym symbolem nieterminalnym, a $\mathcal{R}$ ciągiem terminali i nieterminali

## Formalna Definicja

Każda gramatyka jest tak naprawdę krotką: $(T, N, P, S)$, gdzie:

- $T$ jest zbiorem terminali
- $N$ jest zbiorem nieterminali
- $P$ jest zbiorem produkcji
- $S$ jest symbolem startowym

#### Terminale

Są to symbole końcowe, stałe.
Nie są rozwijane przez produkcje.
#### Nieterminale

Symbole, które można definiować za pomocą produkcji.
Za pomocą produkcji mogą tworzyć ciągi symboli terminalnych i nieterminalnych.
#### Produkcje

Jest to zbiór reguł typu: $L \rightarrow (T \cup N)$ 
#### Symbol Startowy

Wybrany element $S \in N$.

## BNF i EBNF

Standardowe sposób zapisu gramatyk bezkontekstowych:

| Pojęcie                     | BNF                          | EBNF                        |
| --------------------------- | ---------------------------- | --------------------------- |
| Nieterminale                | `<napis>`                    | `napis`                     |
| Terminale                   | Dowolne znaki poza `<` i `>` | Dowolne znaki w cudzysłowie |
| Produkcje                   | `::=`                        | `=`                         |
| Warianty produkcji          | $w_{1} \| w_{2}$             | $w_{1} \| w_{2}$            |
| 0 lub 1 wystąpienie         | –                            | `[x]`                       |
| Dowolnie wiele<br>wystąpień | –                            | `{X}`                       |
