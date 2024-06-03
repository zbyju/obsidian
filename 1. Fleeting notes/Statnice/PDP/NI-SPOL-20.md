**Paralelní algoritmy pro redukci, prefixový součet a segmentový prefixový součet na PRAM, v ortogonálních, hyperkubických a obecných topologiích, aplikace.**

# Paralelni redukce
Vstup:
- Pole n prvku z mnoziny D 
- Mnozina p procesu
- Asociativni a pripadne komutativni operace +: DxD->D
Vystup:
- Skalar S=X\[0\] + X\[1\] ... + X\[n-1\]

Paralelni cas T(n, p) = $\alpha n/p + \beta log p$ (vypocetni + komunikacni)
Dolni mez L(n, n) = $\Omega(log n)$
Je to hyperkubicky algoritmus => optimalni na hyperkubickych sitich

## MPI
- `MPI_Reduce` - All-to-one redukce
	- ![[Pasted image 20240603203020.png]]
	- Funkce si vezme:
		- Vstupni buffer
		- Vystupni buffer
		- pocet prvku
		- typ dat
		- operaci
			- MPI_SUM, MPI_MAX, MPI_LXOR
			- MPI_MAXLOC (globalni maximum + pozici)
			- lze definovat vlastni
		- koren vypoctu (rank)
		- Komunikator
	- Vysledek bude jen v koreni
- `MPI_Allreduce` - All-to-all redukce
	- Funkce si vezme:
		- Vstupni buffer
		- Vystupni buffer
		- pocet prvku
		- typ dat
		- operaci
		- komunikator
	- Vysledek dostanou vsichni
		- Vsichni jsou root, proto neni potreba specifikovat
	- Na pozadi probehne all-to-all broadcast kde si vsichni vymeni svoje data
- `MPI_Reduce_scatter` - 
	- ![[Pasted image 20240603203957.png]]
	- Funkce si vezme:
		- Vstupni buffer
		- Vystupni buffer
		- pocet prvku v sendu
		- typ dat
		- operaci
		- komunikator
	- Redukce se rozdeli mezi procesy rovnomerne

Topologie:
![[Pasted image 20240603205733.png]]
- Hyperkrychle - predavani po kostre
- Binarni strom nebo motylek - redukce z listu
- 1D mrizka - simulace hyperkrychle
- PRAM - redukce kazdeho 2^n prvku
# Prefixovy soucet (scan)
Vstup:
- Pole velikosti n prvku mnoziny D
- Asociativni a komutativni operace + nad D
Vystup:
- Pole vsech prefixovych souctu:
	- Y\[i\] = X\[0\] + X\[1\] + ... + X\[i\]

Napriklad pro counting sort

Je to uplne stejne jako redukce, ale kazdy mezivysledek i zapiseme.
Takto to ale nejde paralelizovat.

Scitame do nasledujicich bunek tak abychom nic nedelali dvakrat.
Po prvnim kroku mame vsechny soucty 1 prvkove
Po druhem kroku mame vsechny soucty 2 prvkove
Po tretim kroku mame vsechny soucty 4 prvkove
...

![[Pasted image 20240603204740.png]]

Trva stejne dlouho jako redukce


## Neprimy strom
Vstupni data v listech, vnitrni uzly pocitaji

Poradi indexace dano poradim listu pri pruchodu do hloubky
Vypocet jako vzestupna vlna nahoru kdy se sectou hodnoty ze synu
Vzestupna vlna inicializuje sestoupnou vlnu do praveho podstromu kam se odesila hodnota z leveho podstromu

Trva max 2\*hloubka stromu

![[Pasted image 20240603210418.png]]

## Primy strom
Hodnoty jsou v listech ale i vevnitr stromu

Indexy pole mapujeme na uzly tak, ze uzly indexujeme POSTFIX.

![[Pasted image 20240603211101.png]]

Algoritmus probiha stejne jako u neprimeho stromu ale hodnoty u vnitrnich uzlu se navic prictou k hodnote ktera se predava nahoru.
## Hyperkrychle
![[Pasted image 20240603211338.png]]
Hodnoty se posilaji ve vlnach vzdy v jedne dimenzi. Kazdy node ma 2 hodnoty zelenou a zlutou.

Kazdy node ma svoje ID (podle hyperkrychle) do obou hodnot si da hodnotu na pozici sveho ID

Posila se v n fazich kde n je dimenze hyperkrychle. Kazdy node posila hodnoty od sebe do sveho souseda v dane dimenzi.

Dostavam zelene a zlute data od souseda:
- Zelena data prictu k mym zelenym datum
- Ke zlutym datum si prectu data zelena od souseda jen pokud mam vyssi adresu
## Mrizka
![[Pasted image 20240603212322.png]]

Adresujeme po radku zleva doprava.

Pak ve trech fazich udelame scan po radcich pak po sloupcich a pak reverzne po radku

Vypocestni rychlost zavisi na velikosti mrizky

## Wormhole mrizka 1D

![[Pasted image 20240603212603.png]]

Krokovani vlastne simuluje binarni strom

Pocet logaritmicky

## Scaled
1. Lokalne udelam prefixovy soucet na sve casti pole
2. Vezmu uplne nejvice pravy prvek
3. Udelam s nim algoritmus popsan vyse
4. Vratim se zpet a updatuju svoje hodnoty

## Aplikace
- RadixSort
- Packing problem
- Paralelni binarni scitacka
- Tridiagonalni system rovnic