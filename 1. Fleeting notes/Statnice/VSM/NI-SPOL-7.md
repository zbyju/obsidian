**Základy teorie informace a kódování, entropie.**

# Entropie
= mira neusporadanosti

## $H(X) = - \sum_{x \in X} p(x) log\ p(x)$
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
(pro kazde x z X)

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

### $H(X, Y) = -\sum_{x \in X}\sum_{y \in Y}\ p(x, y)\ log\ p(x, y)$

nebo vektorove:

diskretni nahodny vektor X se sdruzenym rozdelenim p(x):
$H(X) = - \sum_{x \in X} p(x) log\ p(x)$

## Podminena Entropie
diskretni nahodne veliciny X, Y, sdruzene rozdeleni p(x, y) a p(y|x) = p(x, y)/p(x):

### $H(Y|X) = -\sum_{x \in X}\sum_{y \in Y}\ p(x, y)\ log\ p(y|x) = H(X, Y) - H(X)$

### Vlastnosti
$H(X, Y) = H(X) + H(Y|X)$

## Relativni Entropie
= Kullback-Leiblerova vzdalenost D(p||q)
Diskretni rozdeleni p, q na mnozine X:

### $D(p||q) = \sum_{x \in X} p(x)\cdot log \frac{p(x)}{q(x)}$


0 log 0/0 = 0; 0 log 0/q = 0; p log p/0 = 0 (kdyz je nejaka hodnota 0, tak ji ignorujeme)

meri vzdalenost dvou rozdeleni
- 0, kdyz jsou stejne
- neni symtricka
- neplati trojuhlenikova nerovnost
- D(p||q) >= 0
	- D(p||q) = 0 <=> p=q
## Vzajemna Informace
### $I(X, Y) = \sum_{x \in X}\sum_{y \in Y} p(x,y)\cdot log \frac{p(x, y)}{p(x)\cdot p(y)} = D(p(x, y)||p(x)\cdot p(y))$

Jde tedy o relativni entropii skutecneho sdruzeneho rozdeleni a rozdeleni nezavislych velicin

Vzajemna informace je:
- symetricka
- I(X, Y) >= 0

I(X, Y) = H(X) + H(Y) - H(X, Y)
I(X, X) = H(X)

## Jensenova Nerovnost