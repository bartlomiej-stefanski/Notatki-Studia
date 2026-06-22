Danych jest $n$ kulek oraz $m$ urn.
Badać będziemy prawdopodobieństwa możliwych ustawień kulek w urnach.

#TODO 

## Ograniczanie Maksymalnej Liczby Kulek w Urnie

Dla każdego elementu będziemy wyliczać dwie funkcje haszujące $h_{1},h_{2}$, by następnie umieścić go w kubełku zawierającym mniej elementów.

> Dla find musimy sprawdzić dwa kubełki.

Po tej optymalizacji oczekiwana wartość elementów w urnie wynosi $O(\ln \ln n)$.
