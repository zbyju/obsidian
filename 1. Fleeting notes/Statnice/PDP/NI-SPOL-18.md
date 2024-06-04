**Programování nad distribuovanou pamětí, programový model MPI (vícevláknové procesy, komunikátory, 2-bodové blokující a neblokující komunikační operace, kolektivní operace), paralelní násobení hustých matic, paralelní mocninná metoda.**

# MPI
Predpoklada distribuovanou pamet
Zalozen na systemu zasilani zprav

Vlakno v OpenMP = proces v MPI

Komunikace se provadi pomoci funkci, ktere jsou vlastne zpravy odeslany vsem (nebo jen podmnozine) procesu.

Lze bezet v rezimech:
- Jen MPI
	- Na kazdem jadru/CPU/nodu bezi 1 nebo par MPI procesu, ktere nesdileji pamet
	- Pameljsi
- MPI + OpenMP
	- Na kazdem CPU/nodu bez par MPI procesu a ty se pomoci OpenMP deli na vlakna bezici na jadrech se sdilenou pameti

Jeden proces lze mapovat na:
- Jeden uzel
	- a dale pocet vlaken = pocet jader uzlu
- Jeden procesor
	- (jeden uzel muze mit vice procesoru)
	- a dale pocet vlaken = pocet jader procesoru
	- vetsinou vyssi vykon

Pro integraci s OpenMP je potreba zavolat `MPI_Init_thread` s danou hodnotou

Procesy se radi do skupiny procesu (kazdy je aspon v jedne skupine) a jsou cislovany od 0 (pokud je ve vice skupinach, pak ma vice ID v ramci kazde z nich) = **rank**
## Komunikatory
Kazda MPI funkce potrebuje komunikator - ten urcuje mnozinu procesu v ramci ktere bude funkce komunikovana
- Intra-komunikator
	- asociovany s konkretni skupinou procesu
	- komunikace mezi procesy uvnitr teto skupiny
	- `MPI_COMM_WORLD` - implicitne preddefinovany pro skupinu vsech procesu
- Inter-komunikator
	- asociovany mezi dvema ruznymi skupinami procesu
	- komunikace mezi skupinami

- `MPI_Comm_rank` - vrati cislo procesu v ramci skupiny
- `MPI_Comm_size` - vrati pocet procesu skupiny
## Komunikacni operace
- 2 bodove
	- komunikacni operace mezi dvema procesy
- kolektivni
	- komunikacni operace mezi vsemi procesy s danym komunikatorem

- blokujici
	- funkce je ukoncena (vrati) po dosazeni urciteho stavu komunikace (nemusi byt jeste uplne hotova)
	- U `MPI_Send`:
		- bud bylo odeslano
		- nebo byl buffer prekopirovan do systemoveho buffer k odeslani
		- => buffer v programu muze byt prepsan
- neblokujici
	- funkce je ukoncena hned, dokonceni komunikace je potreba explicitne testovat

Napr.
- `MPI_Send(buffer, count, datatype, destination_rank, tag, komunikator)`
- `MPI_Recv(buffer, count, datatype, source_rank, tag, komunikator, status)`
- Oba blokujici, 2bodove

Lze posilat jen specificke typy dat:
- `MPI_CHAR`
- `MPI_INT`
- `MPI_UNSIGNED`
- `MPI_LONG`
- `MPI_UNSIGNED_LONG`
- `MPI_INT16_T`
- `MPI_UINT64_T`
- `MPI_FLOAT`
- `MPI_DOUBLE`
- nebo je potreba definovat vlastni MPI typ
- zprava musi vzdy zabirat souvisly kus pameti

V ramci statusu dostaneme:
- `MPI_SOURCE` - rank procesu odesilatele
- `MPI_TAG` - tag zpravy
	- muzeme prijmat vsechny tagy a od vsech a pak bychom nevedeli

Tagy:
- `TAG_WORK` - posilam praci
- `TAG_TERMINATE` - uz neni prace ukonci se

Sendy:
- Blokujici
	- `MPI_Send` - standardni send
		- bud odesle a pak vrati
		- nebo prekopiruje a pak vrati
		- nevime ktere
	- `MPI_BSend` - buffered mode
		- uzivatel musi pripravit buffer do ktereho se data prepisou
		- lokalni operace
	- `MPI_SSend` - Synchronous mode
		- K navratu nedojde dokud nedojde k prijeti dat
		- nelokalni operace
	- `MPI_RSend` - Ready mode
		- Deklarujeme ze druha strana je ready
		- Pokud ne tak funkce vrati chybu a chovani neni definovano
		- nelokalni operace
- Neblokujici
	- Ma navic strukturu request, ktera muze byt pouzita navic pro sledovani stavu requestu
	- Pouziva se pokud poradi neni uplne jasne
	- Potrebujeme vice flexibility
	- Chceme prekryvat komunikaci a vypocet

Dalsi funkce:
- Sendrecv - zaroven send a receive
- Probe - zjisti jestli je prisla nejaka zprava ale jeste ji neprijma
	- Dobre pokud nevime velikost zpravy dopredu; muzeme se pripravit
	- Prijem optional zprav ktere necekame

Kazda funkce vraci jeste navratovou hodnotu = chybovy kod nebo `MPI_SUCCESS`

### Kolektivni operace
= jeden -> mnoho
- Vysilani jeden vsem - broadcast (`MPI_Bcast)`)
	- V hyperkrychli poslu sousedovi a ten posila do vyssi dimenze nez odkud to prislo, rekurzivne to vytvori strom
- Vysilani skupine - multicast (`MPI_BCast`)
- Rozesilani jeden vsem - scatter (`MPI_Scatter`)
- Sbirani ode vsech - gather (`MPI_Gather`)

# Nasobeni Hustych Matic vektorem
## Mapovani prouzkove
![[Pasted image 20240603231630.png]]

Rozdelim matici mezi procesy bud:
- blokove (p pruhu)
- cyklicky (po radcich)
- kombinace (k-radku cyklicky)

Procesy tvori 1D mrizku M(p)
(i v pripade sloupcove orientace)

### Radkove
1. Procesy si vymeni sve casti vektoru, tak aby mely cely vektor (all-to-all broadcast)
2. Pronasobi svou cast matice s vektorem
3. Kazdy proces ma nyni cast vysledku
	- Pokud potrebujeme tak musim rozeslat zase vsem ostatnim
### Sloupcove
Stejne jako u radkoveho ale po sloupcich

1. Procesy uz maji svou cast vektoru kterou potrebuji
2. Spocitaji cast
3. Pak museji udelat p redukci operace + (all-to-all redukce)

Ve vysledku stejne rychle jako radkove

## Mapovani Sachovnice
![[Pasted image 20240603232142.png]]

Znovu muzeme:
- blokove
- cyklicky (po bunkach)
- kombinovane (po segmentech)

Procesy tvori virtualni 2D mrizku M(sqrt(p), sqrt(p))
# Nasobeni hustych matic
2 huste matice

Matice jsou namapovane sachovnicove = kazdy proces ma submatici z A a z B a chci aby nakonci mel tu stejnou submatici C
## Naivne
1. Matice A se musi radkove rozeslat
2. Matice B se musi sloupcove rozeslat
3. Roznasobim klasicky
Aritmeticky neni redundance
Pametove neefektivni, potrebujeme vice pameti
## Cannonuv
P procesu, sqrt(P) kroku

Nechci prekrocit pamet, takze misto toho abych vsechno nazacatku ziskal, tak ziskam cast a pak se toho budu zbavovat.

Vypocet je synchronni; provedu vypocet poslu dalsimu procesu a ziskam nove data od predchoziho procesu

1. Radky A zrotuju doleva o i pozic (i = index radku)
2. Sloupce B zrotuju nahoru o i pozic (i = index sloupce)
4. Proces Pij spocita soucin Aij \* Bij - jedna bunka matice C
5. Radek A zrotuju doleva o 1
6. Sloupce B zrotuju nahoru o 1
7. Tohle opakuju dokud nemam vysledek

Jsou na to optimalni 2D toroidy
### Foxuv
P procesu sqrt(P) kroku

Delaji se posuvy
# Paralelni Mocninna Metoda
Algoritmus pro hledani nejvetsiho vlastniho cisla (v absolutni hodnote) matice A a vektoru v: $A\cdot v = \lambda \cdot v$

1. Inicializuj pocatecni vektor x
2. Vynasob A vektorem x cimz vznikne y
3. Spocti normu y
4. Nahrad vektor x normalizovanym vektorem y
5. Vyhodnot kriterium konvergence
6. Pokud splneno zastav, jinak znova 2.

## Libovolne mapovani
P_i potrebuje cely vektor x

Kazdy proces muze vyprodukovat jakykoliv index y_i
=> kazdy proces musi mit naalokovan prostor pro cely vektor y
=> nakonec musime udelat redukci (Allreduce)
=> kazdy proces zna nove y
## Mapovani po radcich
Predpokladame ze kazdy radek ma +- stejne nenul

Vysledek nasobeni pro jeden proces je jen cast vektoru y
=> neni potreba alokovat n prvku, staci n/p
=> kazde proces si pak sesklada (neni potreba reduce) vysledky z ostatnich

-> rychlejsi protoze neni potreba predavat cely vektor y, ale staci cast
## Mapovani Sachovnice 
procesy v 2D mrizce

vektor umistovan na diagonalni procesy
1. je potreba vektor rozeslat sloupcove
2. roznasobit
3. rozeslat vysledny vektor na diagonalu
4. znovu