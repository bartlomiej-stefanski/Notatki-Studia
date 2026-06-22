> Rodzaj *transducera skończonego*

## Definicja

Krotka $\mathcal{M} = <Q, \sum, \Omega, \delta, \chi, q_{0}>$, gdzie:

- $Q$ – skończony niepusty zbiór stanów
- $\sum$ – skończony niepusty zbiór symboli (alfabet)
- $\Omega$ – skończony niepusty alfabet wyjściowy
- $\delta : Q \times \sum \rightarrow Q$ – funkcja przejścia
- $\chi : Q \rightarrow \Omega$ – funkcja wyjścia
- $q_{0}\in Q$ – stan początkowy

Zapis $O(\mathcal{M}) : Q \times \sum^{*} \rightarrow \Omega^{*}$ oznacza *wyjście dla zadanego wejścia i stanu*.
Funkcja wyjściowa $\chi$ ustawia wyjście widząc tylko aktualny stan – wartości wyjściowe *są* w stanach.

Pomijając w notacji $Q$ możemy przyjąć start w stanie początkowym.
> Główną i jedyną różnicą występującą tutaj jest funkcja wyjściowa, która dla każdego stanu ustawi odpowiednie wyjście

## Przykłady

### Liczenie od 0 do 3

$\mathcal{M} = <Q,\sum,\Omega,\delta,\chi,q_{0}> = <\set{0,1,2,3}, \mathbb{B},\set{0,1,2,3},\delta,id,0>$
$$\delta(q,a) = \begin{cases} q : a = 0 \\ (q+1)\ mod\ 4 : a =1 \end{cases}$$Taki automat można przetłumaczyć na następujące tabelki i diagram:
![[Tabelka-DAS-Licznik-4-bitowy.png]]
No i implementacja w [[System Verilog]]:
```systemVerilog
module counter(input clk, rst, a, output [1:0] o);
	logic [1:0] q;               // stan automatu
	always_ff @(posedge clk or posedge rst)
		if (rst) q <= 2'b0;      // stan początkowy
		else q <= a + q;         // funkcja przej±cia
	assign o = q;                // funkcja wyj±cia
endmodule
```
Alternatywnie można skorzystać z [[Mapa Karnaugh]] by uzyskać prostszy układ, który będzie wyglądać jak zwyczajny [[Licznik]] 4-bitowy.

### Wykrywanie Zmian

$\mathcal{M} = <\set{00,01,10,11}, \set{0,1}, \set{00,01,10}, \delta, \chi, 00>$
$\delta = \set{(ca,b,ab) | a \in \set{0,1}, b \in \set{0,1}, c \in \set{0,1}}$  – to jest strasznie dziwny zapis...
$\chi = \set{(00,00),(11,00),(01,01),(10,10)}$

No i tradycyjnie tabelka wraz z diagramem:
![[Tabelka-DAS-wykrywanie-zmian.png]]

Układ można zaimplementować w [[System Verilog]] w następujący sposób:
```systemVerilog
module detect_moore(input clk, rst, a, output [1:0] out);
	logic [1:0] q;                  // stan automatu
	always_ff @(posedge clk or posedge rst)
		if (rst) q <= 2'b0;         // stan pocz¡tkowy
		else q <= {q[0], a};        // funkcja przej±cia
	assign out[0] = !q[1] && q[0];  // funkcja wyj±cia
	assign out[1] = q[1] && !q[0];
endmodule
```
Z czego zostanie wygenerowany następujący układ:
![[Schemat-DAS-Wykrywanie-zmian.png]]
