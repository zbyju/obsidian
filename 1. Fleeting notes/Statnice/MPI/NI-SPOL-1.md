Teorie grup: Grupoidy, pologrupy, monoidy a grupy. Podgrupy, cyklické grupy a jejich generátory.

# Množiny s jednou binární operací
Mějme:
- libovolnou neprázdnou množinu $M \ne \emptyset$
- binární operaci na ní $\circ : M \times M \rightarrow M$
## Grupoid 
1. $\circ : M \times M \rightarrow M$
	- Mnozina M je uzavrena na operaci $\circ$

**Priklady:**
$\mathbb{Z}$
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