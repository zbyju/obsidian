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