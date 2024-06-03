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