**Testování statistických hypotéz. T-testy, testy nezávislosti, testy dobré shody.**

# Statistika
Pravdepodobnost:
1. Udelame model
2. Na zaklade vlastnosti modelu predikujeme realitu
Statistika:
1. Pozorujeme realitu
2. Vybereme vhodny model
3. Odhadujeme parametry model
4. Testujeme hypotezy
5. Porovnavame model s realitou
## Nahodny vyber
n-tice stejne rozdelenych nezavislych nahodnych velicin X1, ..., Xn s distribucni funkci F je nahodny vyber z rozdeleni F.

nezavisle nahodne veliciny = iid

Realizace nahodneho vyber (= vektor nahodnych pozorovani, data) je ntice konkretnich pozorovanych cisel x1, ..., xn

Muzeme provadet:
- Odhad tvaru rozdeleni
	- urceni rozdeleni F s neznamymi parametry $\theta$ 
- Odhad parametru rozdeleni
	- bodovy odhad
		- urceni nejpravdepodobnejsi hodnoty $\theta$
	- intervalovy odhad
		- urceni intervalu ve kterem $\theta$ lezi s vysokou pravdepodobnosti
- Overeni spravnosti model
	- test dobre shody
		- overujeme hypotezy o tvaru rozdeleni
	- parametricke testy
		- vytvorime hypotezu o $\theta$ a rozhodujeme jestli hypotezu muzeme zamitnout
## Interval spolehlivosti
Interval (L, U), urceny statistikou splnujici:
### $P(\theta \in (L, U)) = P(L < \theta < U) = 1 - \alpha$

se nazyva $100 \cdot (1-\alpha)\%$ interval spolehlivosti (konfidencni interval)

Interval (L, inf), respektive (-inf, U), urceny statistikou splnujici:
### $P(\theta \in (L, \infty)) = P(\theta \in (-\infty, U)) = 1 - \alpha$

se nazyva dolni respektive horni (jednotranny) $100 \cdot (1-\alpha)\%$ interval spolehlivosti (konfidencni interval)

Statistika L resp. U se nazyva dolni resp. horni mez intervalu spolehlivosti.
Cislo 1-alpha je hladina spolehlivosti.
# Testovani Hypotez
Formulujeme hypotezy:
- Nulova hypoteza H0 oznacuje tvrzeni, o kterem chceme rozhodovat
- Alternativni hypoteza HA nebo H1 je opacne tvrzeni, ktere stavime proti H0
Predpokladame ze plati bud H0 nebo HA

Test nulove hypotezy proti alternativni hypoteze je rozhodovaci proces zalozeny na hodnote nahodne vektor, na jehoz zaklade bud zamitneme nebo nezamitneme nulovou hypotezu
## Chyby
- Chyba prvniho druhu - zamitnu H0 ackoliv plati
- Chyba druheho druhu - nezamitneme H0 ackoliv neplati (plati HA)

Chci ovladat chybu prvniho druhu - chceme aby byla mensi nez zvolene alpha => volime jako nulovou hypotezu to zavaznejsi; to co chci dokazat volim jako alternativni hypotezu tim si chci byt "jisty"

Test konstruujeme tak aby chyba 2. druhu byla co nejmensi

Zamitnuti H0 ve prospech HA je silny vysledek
- testuju na 95% => vim ze HA je splnena na 95%
- statisticky vyznamne
Nezamitnu H0
- chyba je sice nejmensi mozna, ale nevim jaka
- statisticky nevyznamne
## Kriticky obor
Mnozinu realizaci X, pro ktere delame testovani na hladine alpha skonci zamitnutim H0, nazyvame kritickym oborem $W_\alpha$

$X\in W_\alpha \iff$ zamitame H0 na hladine alpha
$X\notin W_\alpha \iff$ nezamitame H0 na hladine alpha

Hladina alpha znamena, ze chyba 1. druhu je nejvyse alpha:
$P_\theta(X\in W_\alpha)\le \alpha\ pro\ kazde\ \theta \in \Theta_\theta$

testy jsou typicky konstruovany:
$\alpha < \alpha' \implies W_\alpha \subset W_{\alpha'}$
=> pokud zamitnu na alpha pak zamitnu i na alpha'
## p-hodnota
existuje nejaka minimalni hladina vyznamnosti *p*, na ktere lze zamitnout (p-hodnota)

$p=p(X)=inf\{\alpha|X\in W_\alpha\}$
p-hodnota je tedy nahodna velicina; potom co provedu experiment tak se z nej stava cislo (dana realizace)

Je-li p-hodnota mensi nez nase pozadovana hladina vyznamnosti alpha, zamitame H0

p-hodnota je horni mez pro pravdepodobnost, ze pri platnosti H0 bude dalsi realizace X' stejne prizniva zamitnuti jako ta aktualni

p-hodnota mluvi o tech datech co jsme zmerili ne o nahodne velicine, ktera je za tim






