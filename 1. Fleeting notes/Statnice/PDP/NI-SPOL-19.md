**Přímé ortogonální a hyperkubické propojovací sítě paralelních počítačů (definice, vlastnosti, vnořování).**

# Definice
## Topologie
$G_n$ (topologie) = mnozina grafu (= instanci topologie), jejichz velikost a struktura je definovana parametrem $n$ (= velikosti dimenze).

Mohou byt vicedimenzionalni.
### Hierarchicky rekurzivni topologie
instance mensich dimenzi jsou podgrafy instanci vetsich dimenzi
### Inkrementalne skalovatelna topologie
definovana pro vsechna N (N = velikost grafu)
### Castecne skalovatelna topologie
definovana pro nekonecne mnoho N, ale ne vsechna N
### Ridka topologie
Pocet hran = $O(|V(G_N)|)$ - stupen uzlu je omezen konstantou; stupen nezavisi na $n$
### Husta topologie
Pocet hran = $\omega = (|V(G_n)|)$ - stupen uzlu je rostouci funkci $n$
## Grafy
### Kartezsky soucin 2 grafu:
$G = G_1 \times G_2$:
V(G) = $\{[x, y]; x \in V(G_1), y \in V(G_2)\}$
E(G) = $\{ <[x_1, y], [x_2, y]>; <x_1, x_2> \in E(G_1) \} \cup \{ <[x, y_1], [x, y_2]>; <y_1, y_2> \in E(G_2) \}$

- U nodu je potreba si drzet informaci o puvodu nodu ($[x, y]$)
- Nody se vytvori jako kartzesky soucin tech mnozin
- Hrany se vytvori tam kde byla uz predtim
- Zachovaji se vsechny hrany z obou grafu


![[Pasted image 20240603002024.png]]

- Soucin je komutativni a asociativni
- Lze udelat mocninu
### Symetrie
Graf je uzlove symtricky pokud:
$\forall u_1, u_2 \in V(G)\ \exists$ automorfismus f takovy, ze $f(u_1) = u_2$

- Jsou-li G1, G2 uzlove symtricke, pak G1 x G2 je take uzlove symetricky
- Kazdy uzlove symetricky graf je regularni
- Kazdy uzlove symetricky graf ma diam(G) = r(G)

### Vlastnosti
- Delka cesty = P(u, v)
- Vzdalenost = dist(u, v) - delka nejkratsi P(u, v)
- Prumerna vzdalenost = 1/N(N-1) \* soucet vzdalenosti dist(u, v)
- Excentricita u = vzdalenost z u do nejvzdalenejsiho nodu
- Prumer grafu = diam(G) = max excentricita
- Polomer grafu = r(G) = min excentricita
- Uzlove disjunktni cesty = sdili jen zacatek a konec
- Hranove disjunktni cesty = nemaji nic spolecneho

- Uzlovy (hranovy) rez = mnozina uzlu (hran), jejichz odebranim se rozpoji graf
- Uzlova (hranova) souvislost grafu: $\kappa(G)$ = velikost minimalniho uzloveho rezu; $\lambda(G)$ = velikost minimalniho hranoveho rezu
	- Pro libovolny souvisly graf:
	- $\kappa(G) \le \lambda(G) \le \delta(G)$
	- delta(G) = minimalni stupen grafu
- Uzlove (hranove) k-souvisly graf = $\kappa(G)\ (nebo\ \lambda(G)) = k$
- Optimalni souvislost: $\kappa(G) = \lambda(G) = \delta(G)$
- Bisekcni sirka = velikost nejmensiho hranoveho rezu na 2 poloviny
- Bipartitni graf = lze obarvit vrcholy na 2 barvy; kazda hrana spojuje vrcholy ruznych barev
	- vyvazeny bipart. graf = obe barvy maji stejny pocet uzlu
## Pozadavky
- Konstatni stupen uzlu
	- Chceme pouziva male/levne switche 
	- => stupen omezen konstantou
	- = ridka topologie
	- => mala souvislost a velke vzdalenosti
- Maly prumer a malou prumernou vzdalenost
	- snizuje komunikacni spozdeni
- Uzlova symetrie a hierarchicka rekurzivita
	- snazsi navrh algoritmu, protoze nezalezi kde vypocet zacne
- Vysoka souvislost
	- Redundatni cesty kvuli vypadkum
	- Paralelni odesilani po nekolika cestach
- Vnoritelnost jinych a do jinych topologii
	- Efektivnost implementace algoritmu zavisi na existenci efektivniho zobrazeni daneho grafu procesu do propojovaci site
	- Schopnost simulovat efektivne jine topologie
- Podpora pro smerovani a kolektivni komunikacni operace
	- Permutacni smerovani
	- Komunikace jeden vsem (broadcast)
	- Komunikace vsichni vsem

Spodni mez prumeru N-uzlove **ridke** site je $\Omega(log N)$.
=> ridka sit nemuze mit lepsi prumer nez log N
# Ortogonalni topologie
Zmena v jedne dimenzi neovlivni druhou dimenzi

Kartezsky soucin jednoduchych grafu

Reprezentanti:
- Binarni hyperkrychle (hypercubes)
- Mrizky (meshes)
- Toroidy (tori)
## Binarni hyperkrychle dimenze n
Nody reprezentovane binarnim ID o n bitech
Node ma edge do dalsiho nodu pokud se lisi prave v jednom bitu ID

![[Pasted image 20240603010541.png]]

|V(Qn)| = 2^n
|E(Qn)| = n*2^(n-1)
deg(Qn) = n
diam(Qn) = n
bisekcni sirka = 2^(n-1)
dist = hammingova vzdalenost
je hierarchicky rekurzivni
je vyvazeny bipartitni
je uzlove symetricka
neni ridka (je husta)

Plati ze Qn = Qm x Qm; pokud n = m \* m
Napr Q6 = Q3 x Q3

uzlu ve vzdalenosti i od zadaneho uzlu je n nad i

prumerna vzdalenost = n/2

mezi libovolnymi uzly existuje k! nejkratsich cest (k je vzdalenost techto uzlu)

pokud mam cestu, pak rotaci cesty vyrobim dalsi cestu
012 je cesta, pak => 201; 120 jsou take cesty

Je to velmi husty graf; velmi drahe; moc se nepouziva.
## Mrizka
Kartezsky soucin 1D mrizky
Hrana mezi uzli, ktere se lisi prave o jedna

![[Pasted image 20240603010609.png]]

diam(M) = n-ta odmocnina z poctu uzlu
neni regularni => neni symetricka
hierarchicky rekurzivi (kartezsky soucin)
dist = manhattanska vzdalenost

nejpraktictejsi jsou 2D a 3D mrizky

algoritmus smerovani = dimenzne usporadane - poradi ve kterem se bude budovat cesta

je bipartitni

## Toroid
Mrizka + zpetne hrany - kazda linearni hrana je ted kruznice
toroid = kartezsky soucin jednoduchych kruznic


![[Pasted image 20240603011545.png]]

Oproti mrizce je ted:
uzlove symetricka (regularni)
oproti kruznici je vsechno bud krat dva nebo deleno dva (bisekcni sirka, prumer, ...)

deg = 2n
bisekcni sirka = 2 \* mrizka

dist = manhattanska vzdalenost s modulem

bipartitni jen kdyz vsechny kruznice sude delky

trosku se pokazila rekurzivni hierarchie
- toroid neobsahuje jako podgraf n rozmerne toroidy, ale mene rozmerne toroidy

jedna z nejuspesnejsich topologii pro komerni pocitace
# Ridke hyperkubicke site
Vychazeji z hyperkrychle, ale pridaji neco navic, aby to bylo ridke

Vezmou hyperkrychli a nahrazuji jeden node za n nodu v kruznici
## Zabaleny motylek
Mame vrcholy v dvou "dimenzich" i a x
Hrana je mezi vrcholy:
- mezi vrcholy v stejne dimenzi i o modulo jedna rozdilne (kruznice)
- mezi vrcholy v dimenzi x tak, ze:
	- negujeme bit na pozici i pro dimenzi x
	- pricteme module 1 k i
	- to nam da dve hrany z jednoho nodu a dalsi dve hrany prijdou z jineho nodu (hrany jsou ale oboustranne) = 4 hrany

Pocet vrcholu = $n \cdot 2^n$
Pocet hran = $n \cdot 2^{n+1}$
diam = n + n/2
deg = 4
bisekcni sirka = 2^n
neni hierarchicky rekurzivni
vyvazeny bipartitni graf prave tehdy kdyz n je sude
hamiltonovsky graf
uzlove symetricky

prumer je logaritmus poctu uzlu
=> optimalni ridka topologie

2D mrizka ma taky deg = 4, ale diam je odmocnina

![[Pasted image 20240603172215.png]]
## Obycejny motylek
Vezmeme zabaleneho motylka a kruznici v jednom miste prestrihneme

tradujeme hiearchickou rekurzivnost za symetrii

Pocet vrcholu = $(n+1) \cdot 2^n$
Pocet hran = $n \cdot 2^{n+1}$
diam = 2n
deg = 2 nebo 4
bisekcni sirka = 2^n
je hierarchicky rekurzivni (obsahuje 2 instance sebe same o 1 dimenzi mensi)
neni uzlove symetricka

oproti klasicke hyperkrychli muzeme pouzivat z uzlu jen 1 dimenze (nemuzeme negovat jakykoliv bit)

## Normalni hyperkubicke algoritmy
V kazdem paralelnim kroku algoritmu jsou pouzity pouze hrany jedne dimenze
V po sobe jdoucich krocich jsou pouzivany po sobe jdouci dimenze
# Vnoreni
Paralelni algoritmus = mnozina procesu posilajicich si zpravy

Zname:
- velikost a strukturu grafu procesu
- pocitac s distribuovanou pameti a znamou topologii

Jak mapovat procesy na pocitac aby vypocet byl co nejefektivnejsi? (napr. casto komunikujici procesy u sebe)

Vnoreni G -> H
(zdrojovy graf G=(V(G), E(G)); hostitelska sit H=(V(H), E(H)) )
= dvojice zobrazeni ($\varphi, \xi$):
- $\varphi: V(G) \rightarrow V(H)$
- $\xi: E(G) \rightarrow P(H)$
(P(H) - mnozina vsech cest site H)

## Meritka
Maximalni zatizeni = max procesu na jednom procesoru

Expanze vnoreni = kolik procesoru na dany pocet procesu mame (#V(H)/#V(G))

Maximalni dilatace zdrojovych hran v hostitelske siti = 
max delka cesty na kterou se namapovala hrana

Maximalni zahlceni hostitelske hrany = 
max pocet hran namapovanych na hranu v hostitelskem

## Definice
Grafy G a H jsou kvaziizometricke, pokud existuji zanoreni v obou smerech s konstantnimi hodnotami meritek kvality (neroste s dimenzi topologie)

H similuju se zpomalenim h, jestlize kazdy jeden krok vypoctu na G muze byt simulovan v O(h) krocich na H.

G a H jsou vypocetne ekvivalentni, pokud G dokaze simulovat H s konstatnim zpomalenim a naopak.

Kvaziizometricke grafy => vypocetne ekvivalentni (ne naopak)

Jestlize |V(G)| = |V(H)| a load = 1, pak dilatace >= diam(H) / diam(G)

N-uzlova kruznice C muze byt vnorena do jakekoliv N-uzlove site G s load=1, dil <= 3 a ecng = 2

## Vnorovani Grafu
### Mrizka do toroidu 
Mrizka a toroid jsou kvaziizometricke
### Hyperkrychle do mrizky/toroidu
Uvazujme Hyperkrychly $Q_{2k}$
Uvazujme mrizku s rozmery $M(2^k, 2^k)$

Dolni mez na dilataci vnoreni Q2k -> M(2^k, 2^k) s load = 1 je $\frac{2^k-1}{k}$

Mapujeme pomoci:
- Svobodovo mapovani - lexikograficky
	- Prvnich k bitu = k bitu radku
	- Druhych k bitu = k bitu radku
- Karnaughovo mapovani - grayova indexace
- Mortonova krivka
### Mortonova krivka
x a y souradnici vyrobime stridanim sudych a lichych bitu
### Motylci
Obycejny motylek a zabaleny motylek jsou kvaziizometricke
## MPI
MPI muzeme pouzit pro popis grafu algoritmu pro planovac, aby mohl delat lepsi rozhodnuti.

Muzeme rict 3 typy topologii:
- Kartezska `MPI_Cart_Create`
	- vytvori bud 1D mrizku nebo 1D toroid
- Graf `MPI_Graph_Create`
	- vytvori topologii grafu
	- popsany poctem uzlu, jejich stupni a linearizovanym seznamem sousedu
- Distribuovany graf `MPI_Dist_Graph_Create`
	- urci pouze svoje sousedy (vystupni hrany) a to predava MPI funkcim
	- kazdy soused za sebe oznami jak vypada jeho sousedstvi