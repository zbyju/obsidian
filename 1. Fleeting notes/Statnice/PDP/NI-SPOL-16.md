**Výkonnostní měřítka paralelních algoritmů, PRAM model, APRAM model, škálovatelnost.**

# Paralelni pocitac
Skupina propojenych vypocetnich prvku (uzlu), ktere komunikuji a spolupracuji, aby rychleji vyresili jednu ulohu.

Cloud = nekolik zakazniku, nekolik problemu
Paralelni pocitac = jedna velka uloha

## Vrstvy paralelismu
1. Vicevlaknova jadra
	- Jadro vykonava stridave vice vlaken soucasne
2. Vicejadrove procesory
	- asynchronne pracujici jadra uvnitr 1CPU
3. GPUs
	- tisice mensich synchronne pracujicich jader
4. SMP uzly
	- nekolik (desitky) vicejadrovych procesoru se sdilenou pameti
5. Cluster
	- Cluster stovek az desetitisicu vypocetnich uzlu
6. Masivne paralelni superpocitace
	- deseti-statice vypocetnich uzlu propojenych specialnimi sitemi
	- velky cluster
	- nelze propojit jen tak ad-hoc
7. Cloud computing
	- ICT infrastructure, data center
# Architektury
## Rizeni Vypoctu
### SIMD
Single Instruction Multiple Data

Uzly maji lokalni pamet a mohou vymenovat data
Vsechny uzly synchronne prijimaji spolecny proud instrukci, ktere mohou bud provadet nebo ignorovat (podle hodnot lokalnich dat)

SIMD se pouziva bud:
- GPU
- Vektorova rozsireni procesoru
### MIMD
Kazdy vypocetni uzel je samostatny pocitac s unstrukcni a datovou pameti
Jednotlive uzly bezi asynchronne

Jsou schopni pracovat samostatne, ale maji nejakou sdilenou pamet nebo komunikacni propojeni pro teamwork

MIMD:
- vicejadrove procesory
- SMP uzly
- komoditni servery
- cluster
- masivne paralelni pocitace
## Architektura pameti
![[Pasted image 20240601153057.png]]
### Sdilena pamet
Procesor sdili pamet s ostatnimi
Komunikace probiha skrze pamet
- Jeden procesor zapise
- Druhy precte
HW/SW komunikace = Read/Write

![[Pasted image 20240601153111.png]]

### Distribuovana pamet
Kazdy procesor ma svou privatni pamet
- Ma pristup jen do sve pameti
Pro pristup do pameti jineho procesoru ho musi pozadat a ten mu odpovi

HW/SW Komunikace = Send/Receive

![[Pasted image 20240601153123.png]]
### Virtualne sdilena pamet
Prace s distribuovanou pameti je slozita, ale je to reseni jak skalovat

-> vznikla virtualne sdilena pamet = uzivatel pracuje jako kdyby byla sdilena, ale je to jen abstrakce pro nej nad distribuovanou pameti

HW Komunikace = Send/Receive
SW Komunikace = Read/Write

![[Pasted image 20240601153144.png]]

## Propojovaci site
### Pro sdilenou pamet
![[Pasted image 20240601153803.png]]a) klasicka sbernice pro pridani novych CPU
b) sbernice se muze zahltit => pridani switche
c) nejak se to zjednodusi pomoci ne uplneho switche (kaskadove)
- Tezko se implementuje prilis velky krizovy switch - n^2 propojeni
### Pro distribuovanou pamet
![[Pasted image 20240601154048.png]]
a) krizovy prepinac, ale tady uz ma kazdy procesor svoji pamet
b) kaskadovy switch
c) propojeni se sousedy, ktere jsou fyzicky nejak blizko sobe
- musime fyzicky umistit blizko sobe
d) ring + bridge mezi nimi
- realne takto vypada Intel, AMD
## PRAM Model
Abstrakce od realneho zapojeni/architektury; ignorovani detailu

Mnozina $p$ procesoru RAM $P_1, P_2, ..., P_n$
- Kazdy $P_i$ ma svou vlastni pamet - lokalni, soukromou 
- Kazdy $P_i$ zna na svuj index $i$
- Kazdy $P_i$ muze pristoupit do sdilene pameti v O(1) case
	- Reseni konfliktu pristupu do sdilene pameti je potreba explicitne resit
Vstup PRAM algoritmu: $n$ polozek v $n$ bunkach sdilene pameti.
Vystup PRAM algoritmu: $n'$ polozek v $n'$ bunkach sdilene pameti.
PRAM provadi **synchronne** 3 typy operaci:
- (R) Read 
	- read bunky sdilene pameti
- (L) Local operation
	- jakakoliv lokalni operace
- (W) Write
	- zapis bunky do sdilene pameti
Komunikace mezi procesory je jedine pomoci Read/Write operaci!
Doba trvani jedne operace:
- Jednotkovy model
	- Kazda operace trva cas 1
- Globalni model
	- L trva 1
	- RW trvaji konstantni cas $d > 1$

PRAM algoritmus lze zapsat regularnimi vyrazy
- Napr: $<RLW>^k$
### Osetreni konfliktu
- Exclusive Read Exclusive Write
	- 2 procesory nesmeji read nebo zapisovat do stejne bunky sdilene pameti
	- zakaz konfliktu
- Concurrent Read Exclusive Write
	- Soucasna cteni jsou povolena
	- V 1 okamziku muze zapisovat pouze 1 CPU do dane bunky
- Concurrent Read Concurrent Write
	- Procesory muzou zapisovat a cist do stejne bunky
	- Priority CRCW
		- Procesorum jsou prideleny priority
		- Dokonceni zapisu je povoleno jen procesoru s nejvyssi prioritou
	- Arbitrary CRCW
		- Dokonceni zapisu je povoleno pouze nahodnemu procesrou
		- Algoritmus nemuze/nesmi delat zadne predpoklady o poradi
	- Common CRCW
		- Vsem procesorum je povolen zapis pouze tehdy pokud zapis do dane bunky ma stejnou hodnotu pro vsechny CPU
		- Kazdy algoritmus musi zajistit splneni teto podminky
		- Jinak tento stav neni definovan
### APRAM
= Asynchronni PRAM

Procesory pracuji asynchronne (neexistuji centralni hodiny)
Procesory vykonavaji stejne operace:
- READ
- LOCAL
- WRITE

Je nutne provadet explicitni barierovou synchronizaci

Doba pristupu do pameti neni 1

Vypocet = posloupnost globalnich fazi, ve kterych procesory pracuji asynchronne, oddelene barierovou synchronizaci

Dva procesory nesmi pristupovat do stejne bunky sdilene pameti v teze globalni fazi, pokud jeden z nich do ni zapisuje

- Lokalni operace = cas 1
- globalni READ nebo WRITE = cas d
- k po sobe jdoucich globalnich READ nebo WRITE = d + k - 1
	- vyplati se delat streaming = chainovani read/write
- barierova synchronizace = B(p)

d a B jsou neklesajicimi funkcemi p
predpokladame ze: $1 < d < B(p) < p$
- v praxi: $B(p) = O(d \cdot log p)$ nebo $B(p) = O(d \cdot log p / log d)$
Po sobe jdouci globalni READ nebo WRITE jsou zretezeny (implementace pomoci sbernice s rozdelenymi transakcemi)
#### Implementace Bariery
##### Centralni citac $B(p) = O(d \cdot p)$
1. Proces dorazi na barieru, check jestli je v prichozi fazi, inkrementuje citac
2. Je-li citac $< p$, proces se deaktivuje
3. Jinak nastavi barieru do odchozi faze a aktivuje ostatni procesy
4. Posledni aktivovany proces nastavi barieru do prichozi faze
##### Binarni redukcni stromg $B(p) = O(d \cdot log p)$
1. Proces dorazi na barieru, check jestli je v prichozi fazi, inkrementuje citac
2. Ceka az skonci redukce v jeho podstromu
3. Po jejim skonceni posle signal rodici
4. Koren stromu pocka na redukci z obou podstromu a prepne do odchozi faze
5. Procesy se aktivuji ve zpetnem poradi.
=> listy se aktivuji jako posledni
# Mereni slozitosti
$T_A^K(n)$ - casova slozitost/doba vypoctu
- T - cas
- A - algoritmus
- K - problem
- n - velikost vstupnich dat
$SL^K(n)$ - (sekvencni) spodni mez sekvencni casove slozitosti
- K - problem
- = nejhorsi casova slozitost toho **nejlepsiho mozneho** sekvencniho algoritmu pro problem K
- Trivilni spodni mez je dana velikosti vstupnich/vystupnich dat
$SU_A^K(n)$ - (sekvencni) horni mez casove slozitosti
- K - problem
- = nejhorsi casova slozitost **nejrychlejsiho existujiciho** sekvencniho algoritmu pro problem K
A je optimalni pokud zname algritmus ktery je asymptoticky stejne rychly jako spodni mez.

Pro porovnani paralelnich algoritmu musim zajistit stejne podminky:
- sekvencni algo poustim na stejnem HW

$T(n, p)$ - cas, ktery uplynul od zacatku vypoctu do okamziku, kdy posledni procesor skoncil vypocet.

$C(n, p) = p \times T(n, p)$ - paralelni cena vypoctu
- Cena je vzdy asymptoticky stejna nebo vyssi nez horni mez
- Cenove optimalni algoritmus ma asymptoticky stejnou cenu s horni mezi.

$S(n, p) = \frac{SU(n)}{T(n, p)}$ - paralelni zrychleni
- Zrychleni je vzdy mensi nebo rovno $p$
- Paralelni zrychleni je **linearni**, prave tehdy kdyz je asymptoticky rovno $p$
- Superlinearni zrychleni muze nastat diky praktickym omezenim sekvencnich pocitacu
	- Anomalie pri prohledavani stavoveho prostoru
	- Swapovani kvuli nedostatku pameti

$L^K(n, p) = SL^k(n) / p$ - (paralelni) spoedni mez

$E(n, p) = \frac{SU(n)}{C(n, p)} \le 1$ - paralelni efektivnost
- $E(n, p) = \frac{S(n, p)}{p}$ - je to vlastne zrychleni na jadro
- Casto vyjadrujeme v %
- Zvolme $0 < E_0 < 1$ konstantu; pak paralelni algoritmus ma **konstatni efektivnost** pokus $E(n, p) \ge E_0 (E(n, p) = \Omega(1)$

Z definic plyne ze plati ekvivalence mezi
1. cenove optimalni
2. linearni zrychleni
3. konstantni efektivnost
## Paralelni Skalovatelnost

![[Pasted image 20240601181511.png]]

Skalovatelnost = schopnost paralelniho algoritmu drzet paralelni optimalitu pokud p a n rostou nebo klesaji.
### Amdahluv zakon
Kazdy algoritmus se sklada z:
- $f_s$ - sekvencni podil
- $1-f_s$ - paralelizovatelny podil
A paralelizujeme pro pevne n pomoci p > 1 vlaken.

#### $S(n, p) = \frac{T_A(n)}{f_s\cdot T_A(n) + \frac{1-f_s}{p}\cdot T_A(n)} = \frac{1}{f_s + \frac{1-f_s}{p}} \le \frac{1}{f_s}$ 
=> Zrychleni nemuze presahnout $1/f_s$
=> pokud $f_s$ = 10% pak $S(n, p) \le 10$ pro jakekoliv $p$
=> od urcite hranice je jedno kolik procesoru mame, protoze pro ne neni dostatecne dost paralelni prace.

Tento zakon popisuje problem fixni velikosti, ktery nabizi omezeny pocet paralelni prace.
### Gustafsonuv zakon
Tento zakon rika ze s rostoucim p bychom meli zvysovat n.
- Pak inherentne sekvencni cast trva kostantni cas $t_{seq}$ nezavisle na $p$
- Inherentne paralelni cast $t_{par}(n, p)$ bude linearni skalovat s $p$ v case

#### $S(n, p) = \frac{t_{seq}+t_{par}(n, 1)}{t_{seq}+t_{par}(n, p)}$
### Silna skalovatelnost
Meri schopnost algoritmu pro fixni n dosahnout linearniho zrychleni s rostoucim p
- Amdahluv zakon dava omezeni

Alternativne:
Je meritko rychlosti poklesu efektivnosti, pokud p roste a n se nemeni
### Slaba skalovatelnost
Definuje jak se meni paralelni cas s p pro fixni n/p

Alternativne:
Je meritko rustu n takoveho, ze pri rostoucim p zustava efektivnost stejna.
