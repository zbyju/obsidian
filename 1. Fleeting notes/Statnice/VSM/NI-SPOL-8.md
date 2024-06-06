**Markovské řetězce s diskrétním časem. Jejich limitní vlastnosti.**

# Nahodny Proces
$(\Omega, \mathcal{F}, P)$ prevdepodobnostni prostor
$T \subseteq R$ indexova mnozina

System nahodnych velicin:
$X = \{X_t | t \in T\}, X_t:\Omega \rightarrow R$
nazyvame realny nahodny proces

Mnozinu T lze chapat jako cas, casova souslednost je dana usporadanim T

Je-li T nejvyse spocetna, pak mluvime o diskretnim case
Je-li T nespocetna, mluvime o spojitem case

Mnozina stavu S je minimalni podmnozina R, pro kterou $P(X_t \in S) = 1; \forall t \in T$
Jinymi slovy S je spolecna mnozina hodnot velicin $X_t$

S je vlastne sjednoceni vsech oboru hodnot Xt

S muze byt nejvyse spocetna (diskretni)
S muze byt nespocetna (kontinuum)

## Trajektorie Nahodneho Procesu
Nahodny proces lze chapat jako zobrazeni z $\Omega$ do prostoru funkci:
$X: \Omega \rightarrow \{f: T \rightarrow S\}$

Hodnotu $X_t(\omega)$ lze chapat jako hodnotu funkce $X(t; \omega)$ promennych $t \in T$ a $\omega \in \Omega$:

Funkce $X(t, \cdot): \Omega \rightarrow R$ je nahodna velicina
Funkce $X(\cdot, \omega): T \rightarrow R$ je realna funkce promenne $t \in T$

Mejme X nahodny proces a omega elementarni jev, pak funkce f:T->R:
### $f(t) := X_t(\omega); \forall t \in T$

nazyvame trajektorie nebo realizace nahodneho procesu X.
## Spocetna mnozina a diskretni cas
S = N (prirozena cisla), nebo {1, ..., |S|}

Diskretni cas, ktery zacina od 0

Rozdeleni v case n (i z S, n z T):
$p_i(n) = P(X_n = i), p(n) = (p_1(n), p_2(n), ...)$

Matice pravdepodobnosti (n, m z T, i, j z S):
$P_{ij}(n, m) := P(X_m = j| X_n = i); P(n, m) := (P_{ij}(n, m))_{i, j\in S}$
(pravdepodobnost prechodu do stavu j v case m, pokud byl predtim v stavu i v case n)
## Markovsky retezec
Nahodny proces {Xn | n z N0 (prirozene s nulou)} s nejvyse pocetnou mnozinou stavu S nazyvame markovsky retezec s diskretnim casem, pokud splnuje markovskou podminku:

### Markovska podminka
$\forall n \in N\ a\ \forall s, s_0, ..., s_{n-1} \in S$ plati:
#### $P(X_n|X_{n-1}=s_{n-1}, ..., X_1=s_1, X_0=s_0) = P(X_n=s|X_{n-1} = s_{n-1})$

Pravdepodobnost zavisi jen na bezprostredni minulosti

#### Alternativne:
$\forall n, m \in N_0\ a\ \forall s, s_0, ..., s_m \in S$ plati:
#### $P(X_{n+m}|X_{m}=s_{m}, ..., X_1=s_1, X_0=s_0) = P(X_{n+m}=s|X_{m} = s_{m})$

Nemusim se divat jen na bezprostredne predchazejici, ale i o n skoku dopredu.

Vlastne staci znat jen jeden bod te historie

#### Alternativne 2:
![[Pasted image 20240606002227.png]]

Pravdepodobnost ze jsem v case n0 ve stavu 0, n1 ve stavu s1, ..., nk ve stavu k je rovna pravdepodobnosti ze jsem v case n0 byl v s0 a nasledne soucin pravdepodobnostnich prechodu z danych stavu v danych casech.

Pravdepodobnosti nejsou nezavisle (neni to soucin pravdepodobnosti ze jsem ve stavu (to by bylo p_s(n)), ale je to soucin prechodu)
#### Chapman-Kolmogorova rovnice
Pro matice prechodu plati pro vsechna n <= m <= r z N0:
##### $P(n, r) = P(n, m) \cdot P(m, r)$

![[Pasted image 20240606002907.png]]

plati tranzitivita prechodu

pro homogenni markovsky retezec pak:
P(n + m) = P(n) \* P(m)
### Homogenni markovsky retezec
Markovsky retezec je homogenni, pokud pro vsechna n z N a i, j z S plati:
##### $P(X_{n+1} = j| X_n = i) = P(X_i = j|X_0 = i)$

Pro homogenni MR pak definujeme (jednokrokovou) matici prechodu:
##### $P := P(0, 1) = (P(X_1 = j| X_0 = i))_{ij\in S}$

zaroven plati:
##### $P(m, m+n) = P(0, n) = P^n$

$P^n$ budeme znacit jako $P(n)$
$P(n)_{ij}$ budeme znacit jako $P_{ij}(n)$
#### Stochasticka matice
Matice prechodu P je stochasticka:
1. $P_{ij} \ge 0$ - ma nezaporne prvky
2. $\sum_{j \in S} P_{ij} = 1$ - vsechny radky se vyscitaji na 1

Soucin stochasticky matic je stochasticka matice
##### MR - SM
K libovolne ctvercove stochasticke matici P existuje homogenni markovsky retezec s diskretnim casem takovy, ze P je jeho matice prechodu.
##### Pocatecni rozdeleni
Abychom znali homogenni markovsky retezec, tak nam staci znat matici prechodu P a pocatecni rozdeleni p(0)

Pocatecni rozdeleni q je vektor ktery se vyscita na 1

Matici prechodu tedy definujeme celou tridu nahodnych procesu, ktere se lisi svym q:
$P_q(X_0 = 1) = q_i; P_q(X_n = i) = (qP^n)$

##### Zajimava pocatecni rozdeleni
Deterministicke q = (0, 0, ..., 0, 1, 0, ..., 0)

Stacionarni (takove z ktereho neutecu) $\pi$: 
###### 1. $\forall i \in S: \pi_i \ge 0$
###### 2. $\sum_{i \in S} \pi_i = 1$
###### 3. $\pi \cdot P = \pi$

pro stacionarni rozdeleni plati ze:
p(0) = pi => p(n) = pi \* P^n = pi \* P = \pi
#### Trvaly/Prechodny stav
trvaly = rekurentni

Stav i z S je trvaly, pokud:
$P(\exists n \in N: X_n = i | X_0 = i) = 1$

Stav i z S je prechodny, pokud:
$P(\exists n \in N: X_n = i | X_0 = i) < 1$

Trvaly je ze pro vsechny trajektorie se do stavu i nekdy vratim
Prechodny je ze existuji nejake trajektorie ktere se do i uz nevrati
#### Cas prvni navstevy
stavu i z S:
$\tau_i := min\{n \in N | X_n = i\}$

je-li mnozina prazdna pak $\tau_i = \infty$

Pozor n z N ne n z N0 -> ignorujeme nulovy cas

![[Pasted image 20240606153657.png]]

### Klasifikace pomoci casu prvni navstevy
#### $f_{ij}(n) = P(\tau_j = n | X_0 = i); n \ge 1; f_{ij}(0) = 0$
= pravdepodobnost prvni navsteva j, pokud zacinam v i, nastane v case n.

#### $f_{ij} = P(\tau_j < \infty | X_0 = i) = \sum_{n=1}^\infty f_{ij}(n)$
= pravdepodobnost, ze nekdy navstivim j, pokud jsem zacinal v i

=> Stavy je trvaly <=> $f_{ii} = 1$
=> Stavy je prechodny <=> $f_{ii} < 1$
### Stredni doba navratu
do stavu i z S:

![[Pasted image 20240606154546.png]]
= n \* pravdepodobnost ze se tam vratim v n (n je cas navratu)
#### Nulovy a nenulovy stav
i z S je nenulovy, pokud stredni doba navratu je konecna (mu_i < nekonecno)

i z S je nulovy, pokud neni nenulovy (mu_i = nekonecno)
### Periodicita
stavu i z S:
#### $d(i) = gcd\{n\in N | P_{ii} > 0\}$
nejvetsi spolecny delitel casu, kdy se retezec vrati do stavu i

stav je periodicky pokud d(i) > 1
stav je aperiodicky pokud d(i) = 1

=> pro libovolny aperiodicky stav i z S plati:
$lim_{n \rightarrow \infty} P_{ii}(n) = 1/\mu_i$

=> pro libovolny stav j z S pak:
$lim_{n \rightarrow \infty} P_{ji}(n) = f_{ji}/\mu_i$
### Klasifikace pomoci matice P
![[Pasted image 20240606161244.png]]

### Dosazitelnost
![[Pasted image 20240606161359.png]]

Je to relace ekvivalence; lze rozdelit stavy na tridy ekvivalence

Pokud jsou 2 stavy ve stejne tride => jsou oba stejneho typu
### Uzavrene stavy
Mnozina stavu C (podmnozina S) je uzavrena, pokud:
#### $\forall i \in C; \forall j \not\in C: P_{ij} = 0$
= prechod ze stavu v C do stavu mimo C ma pravdepodobnost 0

Pokud ma C jen jeden stav, pak tento stav nazyvame absorpcni

Preusporadejme stavy tak, aby stavy z C byly nakonci:
![[Pasted image 20240606161947.png]]

Mnozina C je nerozlozitelna (ireducibilni) pokud pro vsechna i, j z C plati i <-> j (Vsechny stavy v C jsou vzajemne dosazitelne)

=> mnozinu stavu S lze vzdy jednoznacne rozlozit:

#### $S = T \cup C_1 \cup C_2 \cup C_3 ...$
kde je mnozina vsech prechodnych stavu, a C_i jsou vzajemne disjunktni nerozlozitelne uzavrene mnoziny trvalych stavu

Matici P pak lze zapsat:
![[Pasted image 20240606162351.png]]
kde:
T - ctvercova matice prechodu mezi stavy T
Ci - ctvercove matice prechodu mez trvalymi stavy Ci
Ri - matice prechodu z mnoziny prechodnych stavu do mnoziny trvalych stavu Ci

#### Konecna mnozina S
V retezci s konecnym poctem stavu S:
1. Nemohou byt vsechny stavy prechodne
	1. Existuji alespon jeden trvaly
2. Neexistuji stavy trvale nulove

zaroven pro kazdy stav i z S a mnozinu dosazitelnich stavu z i (=Si):
1. pokud vsechny stavy z Si plati ze i je z nich dosazitelne, pak je i trvaly nenulovy
2. pokud existuje nejaky stav z Si pro ktery i neni dosazitelny, pak je i prechodny
### Stacionarita
Pro nerozlozitelny MR:
1. Jsou-li vsechny stavy prechodne nebo trvale nulove, stacionarni rozdeleni neexistuje
2. Jsou-li vsechny stavy trvale nenulove, stacionarni rozdeleni existuje a je jedine

=> Je-li mnozina stavu S konecna, pak stacionarni rozdeleni existuje

#### Pocet stacionarnich rozdeleni
Celkem bude existovat tolik linearne nezavislych stacionarnich rozdeleni, kolik je nenulovych mnozin C

libovolna konvexni kombinace (jako linearni ale koeficienty >= 0) je zase stacionarni rozdeleni
# Pravdepodobnost Pohlceni

![[Pasted image 20240606165955.png]]

Prvek Uij je pravdepodobnost, ze prvni prvek, ktery me pohlti (prvek z C) bude j, pokud zacnu v i

Prvek Nik je stredni pocet pruchodu stavem k, nez budu pohlcen, pokud zacnu v i
- Pokud je k trvaly, pak tato hodnota bude nekonecno

Prvek Ni. je stredni doba do pohlceni, pokud zacnu v i

N ziskam operace inverze (I - T)
U ziskam operaci NR
N. ziskam vyscitanim po radcich
## Limita Matice T^n
Matice T^n konverguje k nulove matici
- jsou to stavy prechodne, takze nich vyskocime ven
## Limita Matice C^n
Pokud vsechny trvale stavy aperiodicke:
![[Pasted image 20240606181953.png]]
![[Pasted image 20240606182006.png]]
= Na radcich budou naskladane stacionarni rozdeleni
## Limita Matice P^n
![[Pasted image 20240606182302.png]]