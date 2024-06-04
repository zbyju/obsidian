**Základy teorie informace a kódování, entropie.**

# Entropie
= mira neusporadanosti

X - nahodna velicina
*X* - mnozina hodnot, kterych nahodna velicina nabyva

## $H(X) = - \sum_{x \in \mathcal{X}} p(x) log\ p(x)$
- X je diskretni nahodna velicina
- p(x) = P(X=x)
- dodefinujeme 0\*log 0 = 0
	- kdyz p(x) = 0 => v sume pak pricte 0
- da se chapat jako entropie toho rozdeleni 
	- = H(p)
- prosta transformace nemeni entropii
	- g - prosta funkce
	- H(X) = H(g(X))
- zmenou baze logaritmu menim jednotky entropie
	- 2 -> bit
	- 10 -> digit
	- e -> nat
	- zmena baze nemeni usporadani ani jejich vzajemnou velikost

pro konecne velke X: H(X) <= log |X| 
- H(x) = log |X| <=> X ma rovnomerne rozdeleni
### Ocekavana mira neurcitosti
Entropii muzeme chapat jako stredni hodnotu

#### $H(X) = - E\ log\ p(X) = E\ I(X)$

#### Vlastni informace (mira neurcitosti)
I(x) = -log p(x) - vlastni informace
(pro kazde x z *X*)

kdyz nastane hodnota s pravdepodobnosti 1, tak to nenese zadnou informaci (vedel jsem ze se to stane)
kdyz nastane hodnota s pravdepodobnosti 0.0001, tak to nese hodne velkou informaci, protoze jsem to necekal

=> entropie je ocekavana mira neurcitosti/mira informace

### Mira neurcitosti Axiomaticky
1. Mira neucitosti je vzdy nezaporna
2. Mene pravdepodobne javy maji vyssi miru neurcitosti
3. Mira neurcitosti pri pozorovani nezavislych jevu se scita
## Sdruzena entropie
X, Y - diskretni nahodne veliciny se sdruzenym rozdelenim p(x, y)
p(x, y) = P(X=x, Y=y)

### $H(X, Y) = -\sum_{x \in \mathcal{X}}\sum_{y \in \mathcal{Y}}\ p(x, y)\ log\ p(x, y)$

nebo vektorove:

diskretni nahodny vektor X se sdruzenym rozdelenim p(x):
$H(X) = - \sum_{x \in X} p(x) log\ p(x)$

## Podminena Entropie
diskretni nahodne veliciny X, Y, sdruzene rozdeleni p(x, y) a p(y|x) = p(x, y)/p(x):

### $H(Y|X) = -\sum_{x \in \mathcal{X}}\sum_{y \in \mathcal{Y}}\ p(x, y)\ log\ p(y|x) = H(X, Y) - H(X)$

### Vlastnosti
$H(X, Y) = H(X) + H(Y|X)$

## Relativni Entropie
= Kullback-Leiblerova vzdalenost D(p||q)
Diskretni rozdeleni p, q na mnozine X:

### $D(p||q) = \sum_{x \in \mathcal{X}} p(x)\cdot log \frac{p(x)}{q(x)}$


0 log 0/0 = 0; 0 log 0/q = 0; p log p/0 = 0 (kdyz je nejaka hodnota 0, tak ji ignorujeme)

meri vzdalenost dvou rozdeleni
- 0, kdyz jsou stejne
- neni symtricka
- neplati trojuhlenikova nerovnost
- D(p||q) >= 0
	- D(p||q) = 0 <=> p=q
## Vzajemna Informace
### $I(X, Y) = \sum_{x \in \mathcal{X}}\sum_{y \in \mathcal{Y}} p(x,y)\cdot log \frac{p(x, y)}{p(x)\cdot p(y)} = D(p(x, y)||p(x)\cdot p(y))$

Jde tedy o relativni entropii skutecneho sdruzeneho rozdeleni a rozdeleni nezavislych velicin

Vzajemna informace je:
- symetricka
- I(X, Y) >= 0

I(X, Y) = H(X) + H(Y) - H(X, Y)
I(X, Y) = H(X) - H(X|Y)
I(X, Y) = H(Y) - H(Y|X)
I(X, Y) = I(Y, X)
I(X, X) = H(X)

## Jensenova Nerovnost
f - konvexni funkce
X - Nahodna velicina

E f(x) >= f (EX)

# Teorie Kodovani
$\mathcal{X}$ - mnozina zprav
$\mathcal{D^*}$ - mnozina konecnych retezu symbolu D-arni abecedy $\mathcal{D}$
- Zobrazeni $C: \mathcal{X} \rightarrow \mathcal{D}^*$ nazyvame **D-arni kod** diskretni nahodne veliciny X
- Obraz C(x) prvku x z X nazyvame **kodove slovo** prislusejici prvku x
- l(x) = delka kodoveho slova prvku x

## Stredni delka kodu
### $L(C) = \sum_{x \in \mathcal{X}} l(x) \cdot p(x)$

## Nesingularni kod
C je proste

= lisi se zpravy => lisi se kodova slova
## Jednoznacne dekodovatelny kod
Rozsireni C\* kodu C je zobrazeni mnoziny *X*\* do mnoziny *D*\*:
### $C^*(x_1, x_2, ..., x_n) = C(x_1)C(x_2)...C(x_n)$
(konkatinace)

Kod C je jednoznacne dekodovatelny, pokud C\* je nesingularni (je proste)

=> Kdyz mi prijde cela zprava, tak jsem schopen urcit puvodni zpravu
## Instantni (Prefixovy) kod
Kod je instantni pokud zadne kodove slovo neni prefixem jineho kodoveho slova

=> muzu rovnou dekodovat pri prochazeni po bitech

![[Pasted image 20240604190855.png]]

## Kraftova nerovnost
Pro libovolny instantni kod nad D-arni abecedou musi delaky kodovych slov l1, l2, l3, ..., ln splnit nerovnost:

### $\sum_i D^{-l_i} \le 1$

Navic ke kazde n-tici delek, ktere splni tuto nerovnost, existuje instantni kod s kodovymi slovy techto delek

