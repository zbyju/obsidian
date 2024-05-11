**Teorie grup: Grupoidy, pologrupy, monoidy a grupy. Podgrupy, cyklické grupy a jejich generátory.**

# Množiny s jednou binární operací
Mějme:
- libovolnou neprázdnou množinu $M \ne \emptyset$
- binární operaci na ní $\circ : M \times M \rightarrow M$
## Grupoid 
1. $\circ : M \times M \rightarrow M$
	- Mnozina M je uzavrena na operaci $\circ$

**Priklady:**
$(\mathbb{Z}^-, \cdot)$ neni grupoid protoze $\mathbb{a} \cdot \mathbb{b} \notin \mathbb{Z}^-$, pokud $a, b$ jsou zaporna.

## Pologrupa
1. $\circ : M \times M \rightarrow M$
2. $\circ$ je asociativni
	- $\forall A, B, C \in M: (A \circ B) \circ C = A \circ (B \circ C)$
	- Je jedno jak vyraz uzavorkuju (poradi operaci)
## Monoid
1. $\circ : M \times M \rightarrow M$
2. $\circ$ je asociativni
3. existuje neutralni prvek
	- $\exists e; e \in M; \forall a \in M: e \circ a = a \circ e = a$
	- Existuje prvek, ktery po provedeni operace se vsemi ostatnimi prvky vrati ten prvek samotny
## Grupa
1. $\circ : M \times M \rightarrow M$
2. $\circ$ je asociativni
3. existuje neutralni prvek
4. existuji inverzni prvky
	- $\forall a \in M; \exists b \in M: b\circ a = a \circ b = e$
	- Pro vsechny prvky existuje nejaky prvek, ktery po provedeni operace vrati neutralni prvek.
	- *Note: b zavisi na a ($b_a$)*
## Abelovská grupa
1. $\circ : M \times M \rightarrow M$
2. $\circ$ je asociativni
3. existuje neutralni prvek
4. existuji inverzni prvky
5. $\circ$ je komutativni
	- $\forall A, B \in M: A \circ B = B \circ A$
	- Je jedno v jakem poradi prvky napisu

## Tvrzeni
1. V monoidu existuje prave jeden neutralni prvek
2. V grupe existuje ke kazdemu prvku prave jeden inverzni prvek


## Caleyho Tabulka
Tabulka vsech kombinaci vstupu a jejich vystupy
## Caleyho Graf
Graf kde mame vsechny nody; z kazdeho nodu udelame vsechny hrany pro vsechny ostatni hodnoty v mnozine M takove ze $start \circ prvek = end$.

# Podgrupa
G je grupa (M, $\circ$)
H je (N, $\circ$) takova, ze:
1. $N \subset M$
2. (N, $\circ$) je taky grupa
3. ((( ta operace je zuzeni na te mnozine )))

## Trivialni podgrupy
1. Grupa obsahujici pouze neutralni prvek ({e}, $\circ$)
2. Grupa samotna (M, $\circ$)

## Tvrzeni
1. Libovolny prunik podgrup je taky podgrupa
2. Neprazdne H je podgrupou G $\iff \forall a, b \in N: a \circ b^-1 \in N$
3. Asociativity je zachovana pro podgrupy (nemeni se operace)

# Rad grupy
Pokud je grupa G:
- Konecna - pak je to pocet prvku nosice
- Nekonecna - pak je to nekonecno

# Lagrangova Veta
H je podgrupa konecne grupy G
Pak rad H deli rad G

**Priklad**
- $\mathbb{Z}_{12}$ muze mit podgrupy pouze s pocty prvku: 1, 2, 3, 4, 6, 12
- Grupy s prvociselnym radem muzou mit jen trivilani (1, sama sebe) podgrupy
- Pokud mam $g$ rad grupy G a $k$, ktere deli $g$, pak z toho vsak nutne neplyne ze existuje podgrupa radu $k$.

### Sylowova veta
G konecneho radu $g$
$p$ je prvociselny delitel $g$
Pokud $p^k$ deli $g$ ($k \in \mathbb{N}$)
pak grupa G obsahuje podgrupu radu $p^k$

**Priklad**:
- k=1 musi tam byt vsechny podgrupy s prvociselnymi rady


# Generujici mnoziny a Generatory grup

## Grupa generovana mnozinou
G = $(M, \circ)$ grupa
$N \subset M$, $N \ne \emptyset$
$\langle N \rangle := \cap{}{\{H:}$ H je podgrupa G obsahujici N $\}$

$\langle N \rangle$ je **podgrupa generovana mnozinou** N
N je **generujici mnozina** grupy $\langle N \rangle$

Pokud N je jednoprvkova N={a}, pak a nazyvame **generatorem** grupy $\langle a \rangle$


**Priklad:**
- Vlastne rika ze vezmeme nejakou mnozinu N a vytvorime tu nejmensi (proto ten prunik) grupu, ktera obsahuje N.
- Pro Z12 a mnozinu {6} je $\langleN\rangle$ = {0, 6} (musi byt uzavrena + musi tam byt neutralni prvek a vsechny inverze); dalsi moznosti jsou napriklad {0, 3, 6, 9, 12}, ale kdyz se pak udela ten prunik, tak ty prvky vypadnou.
- Pokud hledame generator grupy, pak hledame prvek ktery vygeneruje celou mnozinu (V Z12 je to napriklad 1, 5)

### Mocnina prvku
G = $(M, \circ)$ grupa
e - neutralni prvek
$g \in M$, kladne prirozene n
Pak:
- $g^0 = e$
- $g^n = g \circ g \circ ... \circ g$ (n-krat)
- $g^n \circ g^{-n} = e$
je n-ta mocnina a (-n)-ta mocnina prvku $g$


### "Grupovy obal"
$\langle N \rangle = \{ a^{k_1}_1 \circ  a^{k_2}_2 \circ ... \circ a^{k_n}_n \}; n \in \mathbb{N}; k_i \in \mathbb{Z}; a_i \in \mathbb{N}$
Grupovym obalem jsme schopni ziskat vsechny prvky patrici do N.

Dusledek: $\langle a \rangle = \{ a^{k}; k \in \mathbb{Z}\}$

Timto zpusobem jsem schopny nagenerovat celou mnozinu.

**Priklad:**
- POZOR: k musi byt ze Z aby se tam nagenerovaly vsechny inverze
- Napriklad pro G = (Q, x), N={2, 3}, ⟨N⟩={$2^k×3^j | k,j∈Z$} nam vygeneruje $​1,2,3,6,\frac{1}{2}​,\frac{1}{3}​,\frac{1}{6},…$


### Tvrzeni
- $\mathbb{Z}_n^+$ je rovna $\langle k \rangle; k \in \mathbb{Z}_n^+ \iff$ kdyz $a$, $n$ jsou nesoudelna.


## Cyklicka grupa
Pokud ma grupa nejaky generator ($G=(M, \circ); \exists a \in M; \langle a \rangle = G$), pak je grupa G cycklicka a $a$ se nazyva generator cyklicke grupy G.

### Rad prvku
Je rad grupy, ktery prvek nageneruje
$ord(a) = \# \langle a \rangle$
Alternativne:
g z G grupy; Pokud existuje kladne cele cislo $m: g^m = e$, pak nejmensi takove m je rad prvku. Pokud neexistuje, pak je rad nekonecno.
$g^1 \ne e; g^2 \ne e; ...; g^m = e$; vidime ze g nageneruje prave m prvku.

## Tvrzeni
- $\mathbb{Z}_n^{\times}$ je cyklicka prave kdyz $n$ je 2, 4, $p^k$, $p^{2k}$, p je liche prvocislo, k je kladne prirozene.
- G je cyklicka grupa radu $n$ a $a$ je nejaky generator, pak $a^k$ je take generator prave tehdy kdyz $k$ a $n$ jsou nesoudelna ($gcd(k,n) = 1$)
- $\phi(n)$ (Eulerova funkce) - udava pocet prirozenych cisel mensich nez n, ktera jsou s nim nesoudelna
- V cyklicke grupe radu $n$ je presne $\phi(n)$ generatoru.
	- to je ten pocet exponentu ktere mi vyrobi dalsi generatory
- Rad $\mathbb{Z}_n^{\times}$ je $\phi(n)$
	- Nejake prvky je potreba vyhodit, protoze by nemely inverzi
	- V Z12 napriklad 2 nemuze mit inverzi 
- Pocet generator $\mathbb{Z}_n^{\times}$ je $\phi(\phi(n))$
	- To vnitrni $\phi$ je rad, to venkovni pak pocet generatoru (ktery potrebuje rad jako vstup)

