## High Level

In high-level languages tail recursion can be used when the return value of a function is the result of an another function call.

This is best visible on an example:
```ocaml
let rec rev_append l1 l2 = match l1 with
	[] -> l2
	| a :: l -> rev_append l (a :: l2)
```
Example above will reverse a list. 
Notice how we do nothing with the return value of `rev_append` – this is mandatory for tail recursion.
## Low Level

In assembly, tail recursion can be done by replacing the `call` with `jump` instruction.
This is desired, because:

- memory savings – no need to create a [[Stack Frame]] for the new function
- time savings – no memory allocations and fever jumps
