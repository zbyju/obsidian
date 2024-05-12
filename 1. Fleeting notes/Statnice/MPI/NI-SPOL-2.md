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
- Muzeme pak definovat polynomy i nad telesem ekvivalentne

## Tvrzeni
- def(f(x) * g(x)) = def(f(x)) + deg(g(x))
- Mejme nenulove polynomy f(x), g(x) nad telesem T; Pak existuji jednoznacne urcene polynomy q(x), r(x) taky nad T takove, ze: f(x)=q(x)g(x)+r(x); r(x) je bud nulovy nebo ma stuped stre mensi nez g(x)
- Mam f(x), g(x) nad T, pak h(x) je nejvetsi spolecny delitel polynomu f(x) a g(x) pokud:
	- h(x) deli f(x)
	- h(x) deli g(x)
	- kazdy polynom ktery deli f(x) i g(x) deli i h(x)
		- h(x) neni jednoznacny; jednoznacny je jeho stupen
- **Bezoutova rovnost pro polynomy**: f(x), g(x) nenulove nad T, pak existuji u(x), v(x) na T takove, ze: gcd(f(x), g(x)) = u(x)f(x)+v(x)g(x)
- $p(\xi)= \sum a_i \cdot \xi^i=0 \iff$ 
- Mame nenulovy p(x) nad T stupne $n$, prvek $\xi \in T$ je koren p prave tehdy
