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

Rozdeleni je urceno parametrem $\theta \in \Theta \subset R$.

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

$p=p(X)=inf\{\alpha|X\in W_\alpha\}$ (inf = nejvetsi z dolnich zavor)
p-hodnota je tedy nahodna velicina; potom co provedu experiment tak se z nej stava cislo (dana realizace)

Je-li p-hodnota mensi nez nase pozadovana hladina vyznamnosti alpha, zamitame H0

p-hodnota je horni mez pro pravdepodobnost, ze pri platnosti H0 bude dalsi realizace X' stejne prizniva zamitnuti jako ta aktualni

p-hodnota mluvi o tech datech co jsme zmerili ne o nahodne velicine, ktera je za tim

Pokud plati H0 => p-hodnota ma Unif(0, 1) rozdeleni (rovnomerne)
## Typy hypotez
- parametricke
	- rozdeleni je urceno parametrem $\theta \in \Theta \subset R^d$
	- tvrzeni se tykaji hodnot $\theta$
- neparametricke
	- X ma obecne rozdeleni, $\Theta \not\subset R^d$
	- Tvrzeni se tykaji ruznych vlastnosti rozdeleni (hodnota medianu, nezavislost), tvaru celeho rozdeleni (test dobre shody)

- jednoduche - obsahuje jedno rozdeleni (stredni hodnota = 5)
- slozena - obsahuje vice rozzdeleni (stredni hodnota >= 5)

![[Pasted image 20240605162525.png]]

### Parametricke testy
#### Jednoducha parametricka hypoteza
proti oboustranne alternative:
$H_0: \theta = \theta_0\ vs\ H_A: \theta \ne \theta_0$

Vytvorime 100(1-alpha)% konfidencni interval (L(X), U(X)) pro parametr theta sestaveny na zaklade nahodne vyberu X, plati:
$P_\theta(\theta \in (L, U)) = 1 - \alpha$

Priklad pro testovani hypotezy o stredni hodnote; prumer = 0.73; stredni hodnota = 0?; konfidencni interval 95% okolo prumeru; je stredni hodnota v konfidencnim intervalu?
![[Pasted image 20240605162632.png]]

Velikost intervalu je dana velikosti alpha a rozptylem dat.

- Zamitneme H0, jestlize $\theta_0 \not\in (L, U)$
	- => chyba prvniho druhu je alpha
- Nezamitneme H0, jestlize $\theta_0 \in (L, U)$

### Slozena parametricka hypoteza
proti jednostranne alternative

podobne jako u predchoziho, ale delame jednostranne intervaly spolehlivosti

![[Pasted image 20240605163531.png]]


# Testove statistiky
Sestrojime statistiku $T \equiv T(X)$ - funkce nahodne vektoru X, u ktere pri platnosti nulove hypotezy zname jeji rozdeleni = testova statistika.

V oblasti moznych hodnot T vybereme podmnozinu $S_\alpha$, pro kterou:
$sup_{\theta \in S_\alpha} P_\theta(T \in S_\alpha) \le \alpha$

pri platnosti H0 ma T hodnoty v $S_\alpha$ s pravdepodobnosti nejvyze $\alpha$

1. Namerim data
2. Vlozim do krabicky "testova statistika", ktera mi da cislo
3. Podivam se jestli cislo lezi nebo nelezi v kriticke oblasti
4. Zamitnu pokud lezi, nezamitnu pokud nelezi
### Kriticka oblast 
= $S\alpha$
Pokud T je v kriticke oblasti => zamitneme H0
Pokud T je mimo kritickou oblast => nezamitneme H0

Kriticka oblast definuje kriticky obor testove statistiky
## Test o Stredni Hodnote Normalniho Rozdeleni
Nahodny vyber X1, ..., Xn z normalniho rozdeleni $N(\mu, \sigma^2)$
### Zname rozptyl
Prumer iid s normalnim rozdelenim $N(\mu, \sigma^2)$ tak ma rozdeleni $N(\mu, \sigma^2/n)$
#### $T = \frac{\overline{X_n} - \mu_0}{\sigma/\sqrt{n}} \sim N(0, 1)$

Pr. testuju, jestli $\mu = \mu_0$ a volim intervaly tak, aby chyba 1. druhu byla alpha => Zvolit kritickou oblast tak, aby pokud neplati H0, tak jsem mel pravdepobobnost, ze se trefim do kriticke oblasti rovnou alpha

![[Pasted image 20240605172216.png]]

Pro test $H_0: \mu \le \mu_0\ vs\ H_A: \mu > \mu_0$, pokud H0 neplati, pak bude prumer vychazet vyssi nez $\mu_0$ a testovat statistika vychylena doprava. Volime tedy jednostranny interval tak, aby pravdepodobnost 1. chyby byla alpha.
### Neznamy rozptyl 
#### $T = \frac{\overline{X_n} - \mu_0}{s_n/\sqrt{n}} \sim t_{n-1}$
kde s_n je odhad smerodatne odchylky; t_n-1 je studentovo rozdeleni s n-1 stupni volnosti
### Shrnuti
![[Pasted image 20240605174009.png]]
## Parovy t-test
Pozorujeme dve hodnoty naraz: $(X_1, Y_1)^T, ..., (X_n, Y_n)^T$ iid (kazdy vektor s ostatnimi) x dvojrozmerneho rozdeleni s neznamym vektorem strednich hodnot $(\mu_1, \mu_2)^T$

Chceme zkoumat, ze:
$H_0: \mu_1 = \mu_2$

Polozime $Z_i = X_i - Y_i$ a budeme zkoumat Z1, ..., Zn, ktere jsou iid.

A budeme zkoumat, ze:
$H_0: \mu_z = 0$
## Dvouvyberovy t-test
Podobny parovemu, ale mame 2 sady dat, ktere jsou na sobe nezavisle

X1, ..., Xn z Normalniho rozdeleni $N(\mu_1, \sigma^2_1)$
Y1, ..., Yn z Normalniho rozdeleni $N(\mu_2, \sigma^2_2)$
Vektory X, Y jsou na sobe nezavisle

### Stejne rozptyly
$\sigma_1^2 = \sigma_2^2$

##### $T = \frac{\overline{X}-\overline{Y}}{s_{12}}... \sim t_{n+m-2}$, kde s12 > 0

![[Pasted image 20240605180920.png]]
### Ruzne rozptyly
(nezname rozptyly, nic o nich nepredpokladame, ani to ze jsou rozdilne)

![[Pasted image 20240605181023.png]]

jiny pocet stupnu volnosti, jmenovatel jiny
## Multinomicke rozdeleni
Mame nahodny vyber X1, ..., Xn (velikost n)
Muzeme vytvorit nahodne veliciny N1, ..., Nk, kde Ni je cetnost hodnot i mezi Xj

tomuto rikame multinomicke rozdeleni
## Test $\chi^2$
### Pri znamych parametrech
Mame nahodny vyber X=X1,..., Xn z diskretniho rozdeleni p'
Cetnosti N1, ..., Nk hodnot X maji multinomicke rozdeleni M(n, p')

Chceme testovat hypotezu H0 ze skutecne hodnoty pravdepodobnosti jsou z rozdeleni p

H0: p'=p

#### $\chi^2 = \sum_{i=1}^k \frac{(N_i - np_i)^2}{np_i}$

![[Pasted image 20240605184656.png]]

### Pri neznamych parametrech
Chci testovat, jestli jsou data z nejake rodiny rozdeleni s neznamymi parametry

Provadime stejnou statistiku jako pri znamych parametrech ale pro libovolne $\theta$. Samotnou statistiku provadime na takovem theta ktere minimalizuje hodnotu statistiky

![[Pasted image 20240605192900.png]]

## Test nezavislosti v kontingencnich tabulkach
Mejme nahodny vektor $X=(Y, Z)^T$ s diskretnim rozdelenim; velicina Y ma r hodnot, velicina Z ma c hodnot

$p_{ij} = P(Y=i, Z=j)$ - sdruzena pravdepodobnost
$p_{i\bullet} = P(Y=i) = \sum_j p_{ij}$ - marginalni pravdepodobnost
$p_{\bullet j} = P(Z=j) = \sum_i p_{ij}$ - marginalni pravdepodobnost

Uvazujeme nahodne vyber z rozdeleni X o velikosti n a oznacme $N_{ij}$ pocet prvku kdy nastala dvojice (i, j)

Hodnoty Nij nazyvame kontingencni tabulka
A marginalni cetnosti jsou:

$N_{i\bullet} = P(Y=i) = \sum_j N_{ij}$ - marginalni cetnost
$N_{\bullet j} = P(Z=j) = \sum_i N_{ij}$ - marginalni cetnost

Vytvorime matici pravdepodobnosti, kterou vyjadruje, jak by kontingencni tabulka mela vypadat, pokud jsou veliciny nezavisle.
### $H_0: p_{ij}=p_{i\bullet} p_{\bullet j}$

![[Pasted image 20240605194037.png]]

Pri platnosti H0 by Nij = (Ni.\*N.j)/n

![[Pasted image 20240605194413.png]]

