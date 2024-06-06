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
#### Homogenni markovsky retezec
Markovsky retezec je homogenni, pokud pro vsechna n z N a i, j z S plati:
##### $P(X_{n+1} = j| X_n = i) = P(X_i = j|X_0 = i)$

Pro homogenni MR pak definujeme (jednokrokovou) matici prechodu:
##### $P := P(0, 1) = (P(X_1 = j| X_0 = i))_{ij\in S}$

zaroven plati:
##### $P(m, m+n) = P(0, n) = P^n$

$P^n$ budeme znacit jako $P(n)$
$P(n)_{ij}$ budeme znacit jako $P_{ij}(n)$
### Stochasticka matice
Matice prechodu P je stochasticka:
1. $P_{ij} \ge 0$ - ma nezaporne prvky
2. $\sum_{j \in S} P_{ij} = 1$ - vsechny radky se vyscitaji na 1

Soucin stochasticky matic je stochasticka matice
#### MR - SM
K libovolne ctvercove stochasticke matici P existuje homogenni markovsky retezec s diskretnim casem takovy, ze P je jeho matice prechodu.
#### Pocatecni rozdeleni
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











