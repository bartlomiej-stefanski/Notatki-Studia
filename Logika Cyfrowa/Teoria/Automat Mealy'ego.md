## Definicja

Krotka $\mathcal{M} = <Q, \sum, \Omega, \delta, \chi, q_{0}>$, gdzie:
- $Q$ – skończony niepusty zbiór stanów
- $\sum$ – skończony niepusty zbiór symboli (alfabet)
- $\Omega$ – skończony niepusty alfabet wyjściowy
- $\delta : Q \times \sum \rightarrow Q$ – funkcja przejścia
- $\chi : Q \times \sum \rightarrow \Omega$ – funkcja wyjścia
- $q_{0}\in Q$ – stan początkowy

Wszystkie [[Automat Moore'a]] są też automatami Mealy'ego.

Zapis $O(\mathcal{M}) : Q \times \sum^{*} \rightarrow \Omega^{*}$ – wyjście dla zadanego wejścia i stanu
Funkcja wyjściowa $\chi$ ustala wyjście patrząc przy okazji na poprzedni stan – wartości wyjściowe *są* na strzałkach.

## Przykłady

### Wykrywanie Zmian

$\mathcal{M} = <\set{s_{0},s_{1}}, \set{0,1}, \set{0_{-},0_{\uparrow},0_{\downarrow}, \delta,\chi,s_{0}}$
$\delta = \set{(s_{b},a,s_{a}) | a\in\set{0,1}, b\in\set{0,1}}$
$\chi = \set{(s_{0},0,o_{-}),(s_{1},1,o_{-}),(s_{0},1,o_{\uparrow}),(s_{1},0,o_{\downarrow})}$

Tabelka i diagram:![[tabelka-DAS-zmiany-mealy.png]]
Tylko jedna tabelka, bo $\chi$ zależy od $Q$ więc są w tym samym miejscu.

Implementacja w [[System Verilog]] może wyglądać następująco:
```systemVerilog
module detect_mealy(input clk, rst, a, output [1:0] out);
	logic q;                  // stan automatu
	always_ff @(posedge clk or posedge rst)
		if (rst) q <= 1'b0;   // stan początkowy
		else q <= a;          // funkcja przej±cia
	assign out[0] = !q && a;  // funkcja wyjścia
	assign out[1] = q && !a;
endmodule
```
Dla tego kodu zostanie zsyntetyzowany następujący układ:
![[Schemat-DAS-zmiany-mealy.png]]
Warto zauważyć, że jest to układ o jeden [[Przerzutniki#Przerzutnik D|DFF]] mniejszy od tego prezentowanego w [[Automat Moore'a]] – tak jest dlatego, że tutaj output możemy dać *zmieniając* stan, a nie tylko czytając stan (wtedy trzeba poczekać dodatkowy cykl na ustalenie się stanu)