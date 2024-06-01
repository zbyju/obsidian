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

