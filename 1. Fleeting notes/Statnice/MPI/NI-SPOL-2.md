**Tělesa a okruhy: Základní definice a vlastnosti. Konečná tělesa. Okruhy polynomů, ireducibilní polynom.**

# Okruh
M neprazdna mnozina
$+, \cdot$ - binarni operace na teto mnozine
Pak:
$R=(+,\cdot)$ je okruh, pokud:
1. $(M, +)$ je abelovska grupa
2. $(M, \cdot)$ je monoid
3. plati levy a pravy distribucni zakon
	- $\forall a, b, c \in M: (a \cdot (b + c) = ab + ac \wedge (b + c) \cdot a = ba + ca)$

## Specialni okruh
- ({0}, +, \*) - trivialni okruh
- (Z, +, \*) - okruh
- (N, +, \*) - neni okruh (N, +) neni grupa

# Teleso
Okruh T = (M, +, \*) je teleso, pokud:
- $(M \setminus {0}, \cdot) je abelovska grupa

## Specialni okruhy
- ({0, 1}, +, \*) - trivialni teleso
- $(\mathbb{Z}, +, \cdot)$ - neni teleso; \* neni multiplikativni grupa
- $(\mathbb{Q}, +, \cdot)$ - je nejmensi ciselne teleso

# Polynom nad Okruhem
Mejme R okruh
$a_i \in R; i = 0, 1, …, n$
$P(x) = \sum^{n}_{i=0}a_ix^i$
je polynom nad okruhem R (s formalni promennou x)

- $a_i$ jsou koeficienty polynomu P(x)
- x je formalni promenna
- Polynomy se rovnaji pokud se rovnaji vsechny koeficienty
- Pokud existuje $k \in {0, 1, …, n} takove, ze $a_k \ne 0$, pak nejvetsi z techto $k$ je stupen polynomu
	- deg(P(x))
	- Pokud P(x) = 0 pak je to nulovy polynom a jeho stupen je nedefinovany

## Tvrzeni
- def(f(x) * g(x)) = def(f(x)) + deg(g(x))
- 
