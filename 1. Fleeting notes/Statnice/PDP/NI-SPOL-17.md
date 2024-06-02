**Programování nad sdílenou pamětí, programový model OpenMP, datový a funkční paralelismus, synchronizace vláken, vícevláknové algoritmy (násobení polynomů, násobení matic a vektorů, řazení).**

# OpenMP
High-level API pro programovani vicevlaknovych aplikaci nad (virtualne) sdilenou pameti (neumi distribuovanou -> MPI).

Zahrunuje 3 casti:
- Parametrizovatelne direktivy pro prekladac
- Systemove (globalni) promenne
- Knihovnu nejcastejsich operaci runtime prostredi

Zakladni model je fork-join:
- Programator explicitne kontroluje paralelni vypocet
- Zacne se sekvencne
- Dale muzeme jednotlive casti algoritmu provadet paralelne a zase joinovat
	- = pararelni oblasti/regiony
- Zaroven je mozne vyuzit thread pool pro snizeni rezie
## Direktivy
```cpp
// Jen sekvencni vlakno

# pragma omp direktiva klauzule1 klauzule2
{
	// Blok
}

// Jen sekvencni vlakno
```
### Parallel regions
`#pragma omp parallel [klauzule]`

Klauzule:
- `if(podminka)` pokud je podminka false, pak se blok provede sekvencne
- `num_threads(expression)` urceni poctu vlaken
- `default(shared|none)`
- `private(list)`
- `firstprivate(list)`
- `shared(list)`
- `copyin`
- `reduction(operator:list)`
	- Zbytek jsou vsechno nastaveni vlastnosti promennych

Vlakno ktere narazi na parallel se stane hlavnim (master) s indexem 0
V bloku se neda menit velikost a poradi vlaken.

Vytvareni paralelnich regionu se muze rekurzivne opakovat (pak je master zvolen ten, ktery na region narazil). Hloubka zanoreni se da ridit `mpt_set_max_active_levels`.

Na konci kazdeho paralelniho bloku je skryta implicitni bariera.

Havarie jednoho vlakna = konec programu

#### Vlastnosti promennych
- `default(shared|none)`
	- Shared - defaultni nastaveni je shared
	- None - vsechny promenne museji mit nastavene
- `private(list)`
	- kazda promenna v seznamu se stava lokalni promennou ve vlaknech
		- kazde vlakno dostane svou vlastni instanci teto promenne, ktera je *neicializovana*
		- platnost je omezena na danou oblast
		- po skonceni oblasti ma promenna puvodni hodnotu
- `firstprivate(list)`
	- stejne jako `private` ale hodnota v kazdem vlaknu je inicializovana na hodnotu pred vstupem do bloku
- `shared(list)`
	- kazda promenna je sdilena vsemi vlakny
		- programator musi zajistit spravny pristup
- `copyin`
	- pouzite hlavne s `threadprivate`
	- inicializuje hodnotu na hodnotu v hlavnim vlakne
- `reduction(operator:list)`
	- hodnota promenne vsech vlaken je na konci bloku redukovana do jedne hodnoty a vysledek zapsan do puvodni promenne
		- operatory: `+ * - & ^ | && ||`
		- hodnota vsech promennych v paralelnim bloku je inicializovana na nulovy prvek
	- promenna by mela mit vlastnost monoidu
		- asociativita je potreba, protoze je potreba kombinovat hodnoty bez zavislosti na poradi
			- fakticka asociativita neni zarucena (napriklad u float operaci kvuli zaokrouhlovani)
		- nulovy prvek je pouzit pro inicializaci
	- nelze kombinovat s task paralelismem
- `threadprivate(list)`
	- podobne jako private, ale hodnota je zapamatovana mezi jednotlivymi paralelnimi bloky
		- je potreba aby vsechny paralelni bloky mely stejny pocet vlaken
	- `copyin` je potreba pouzit pri vstupu do prvniho bloku pro inicializaci promenne

Vlastnosti nastavene na pointery se vztahuji pouze na pointer samotny; ne na jejich value.
#### Stanoveni poctu vlaken
Vlakna jsou cislovana 0 az p-1

Pocet vlaken je rizen v tomto poradi:
1. vyhodnoti se klauzule `if`
2. hodnota vyrazu `num_threads`
3. hodnota procedury `omp_set_num_threads`
4. hodnota systemove promenne `OMP_NUM_THREADS`
### Typy paralelnich bloku
OpenMP podporuje nekolik typu paralelnich vypoctu:
- datovy/iteracni paralelismus
	- kombinace s cyklem for
- funkcni/task paralelismus
	- kombinace s rekurzi

#### Iteracni/datovy paralelismus
`# pragma omp for []` nebo `pragma omp parallel for`
(je vytvorena vyjimka pro dve klauzule na radek)

Klauzule:
- `schedule(typ, {chunk_size})`
	- `static` - jsou prideleny po sobe jdouci bloky iterace
		- pokud je chunk_size definovan pak udava velikost
			- napr:
				- p=3
				- chunk_size=1
				- i1->p1, i2->p2, i3->p3, i4->p1, ...
		- pokud ne pak je blok velikosti n/p
	- `dynamic` - bloky jsou pridelovany dynamicky na pozadani
		- chunk_size udava kolik pri kazdem prideleni vlakno dostane
		- pokud neni chunk_size uveden pak = 1
	- `guided` - bloky maji velikost $x = max(ceil(\#\ dosud\ nepridelenych\ iteraci / p), chunk_size)$
		- chunk_size defaultne = 1
	- `runtime` - zpusob prideleni je zvolen na zaklade systemove promenne `OMP_SCHEDULE`
	- `auto` - vyber je prenechan na kompilatoru
- `collapse(i)`
	- kolik urovni = i ma zkolabovat do jednoho velkeho cyklu
- klauzule pro promenne
- `ordered`
- `nowait` - na konci se neceka na bariere
#### Funkcni/task paralelismus
`# pragma omp task [klauzule]`
=vygeneruje novou ulohu volanim dalsi funkce paralelne

vlakna vytvareji ulohy, pak skonci a berou dalsi ulohu z task poolu.

Klauzule:
- `if(podminka)`
	- pokud false, pak ji dane vlakno hned vykona (tim pozastavi vykonavani stavajiciho tasku)
- klauzule pro promenne
- `final(vyraz)`
	- pokud je vyraz true pak je uloha finalni a uz se nebudou generovat dalsi tasky
- `priority(vyraz)`
	- priradi prioritu

`# pragma omp taskwait` - rodicovska uloha ceka na vykonani synovskych uloh
`# pragma omp single` - direktiva pro zahajeni vypoctu pomoci jednoho vlakna

### Synchronizace vlaken
Na konci kazdeho paralelniho bloku je bariera.

Dale muzeme pouzit explicitne:
- `barrier`
- `master` - blok muze vykonat jen master
- `single` - blok muze vykonat jen jedno libovolne vlakno
- `critical` - kriticka sekce, kde se muze nachazet jen jedno vlakno soucasne
- `atomic` - atomicka operace
- `taskwait` - pockani na vykonani vsech synovskych tasku
# Nasobeni polynomu
Sekvencni:
![[Pasted image 20240602154006.png]]

3 moznosti jak paralelizovat:
1. podle i
2. podle j
3. podle index i+j (vystupniho pole $C$)

## Podle i
Kazde vlakno dostane cast prvniho polynomu a probiha cely druhy polynom a pricita nasobky.

Problemy:
- 2 vlakna mohou pristupovat do stejneho indexu C
	- je potreba atomic update
- false sharing bude, protoze 2 vlakna mohou zapisovat vedle sebe (hlavne uprostred C)

![[Pasted image 20240602154117.png]]

## Podle j
Kazde vlakno ma vzdy stejne i a projizdi spolu indexy i

Vylepseni:
- Dve vlakna nemohou zapisovat do stejne bunky (i maji stejne, j maji rozdilne => i + j bude jine)

Problemy:
- Falesne sdileni bude:
	- je mozne to sice alignout, ale v kazde iteraci se nam posune kam budeme zapisovat s danym vlaknem
	- nelze se vyhnout falesnemu sdileni
- Hodne implicitnich barier na konci kazde iterace



![[Pasted image 20240602154416.png]]

## Podle i+j
Prochazime pole podle souctu indexu pro primou indexaci do vystupniho pole C.

Vylepseni:
- Jen jedna bariera na konci
- Zadny atomic update

Problem:
- Rozlozeni zateze vlaken
	- i+j=0 je pouze pro i=0, j=0; i+j=5 je pro 0,5;1,4;2,3;3,2;4,1;5,0
	- lze resit zvolenim vhodneho chunk_size aby byla rovnomerna zatez

![[Pasted image 20240602154847.png]]

# Nasobeni matic
## Huste matice
Mame huste matic A, B velikosti nxn pomoci klasickeho algoritmu n^3 operaci nasobeni.

![[Pasted image 20240602155511.png]]
### Podle i
Vyhody:
- Jen jedna bariera
- Kolize nejsou => Zadne atomic
- Zadne falesne sdileni (pokud udelame align)


![[Pasted image 20240602155847.png]]

### Podle j
Vyhody:
- Kolize nejsou
- Nemelo by dochazet k falesnemu sdileni
Problem:
- Rezie s barierama

### Podle k
Problemy:
- Hlavni vlakno dela n^2 iteraci
	- n^2 barier
Hruza
## Ridke matice (krat vektor)
A - ridka matice nxn
x - vektor kterym nasobim velikosti n
y - vystupni vektor velikosti n
N - pocet nenul
### COO
Matici reprezentujeme jako 3 pole:

RowInd = pole y souradnic
ColInd = pole x souradnic
Elems = pole hodnot

![[Pasted image 20240602164412.png]]

Sekvencni kod: ![[Pasted image 20240602164508.png]]
### Podle kazde nenuly
Nevyhody:
- Neprima adresace -> skaceme ve vsech polich (krome Elems)
	- => kolize -> atomic update
- Bude dochazet k falesnemu sdileni

![[Pasted image 20240602164636.png]]

## CSR
Porad mame 3 pole:
- RowStart - index zacatku daneho radku v poli ColInd
- ColInd - x souradnice nenuly
- Elems - hodnota


![[Pasted image 20240602164824.png]]
Sekvencni kod:![[Pasted image 20240602165123.png]]
### Podle radku
Paralelizujeme pro kazdy radek


![[Pasted image 20240602165406.png]]
# Paralelni Razeni
## Quicksort
Sekvencni verze: ![[Pasted image 20240602191745.png]]
Potrebujeme:
- swap - prochozeni dvou cisle
- volba pivota
	- posledni prvek je pivot
	- chytreji
- partition - rozdeleni na 2 partition
	- leva - mensi nez pivot
	- prava - vetsi nez pivot

### Vylepseni
1. Nahrazeni posledni rekuze za iteraci
	- Nahrazeni `if` za `while`
2. Zavedeni prahu velikosti pole pro vytvareni OpenMP uloh
	- Pokud je pole prilis male, pak se nevyplati 
3. Paralelizace partition

## Partition
Lepsi verze je Hoare:
- Mam:
	- Pivot - posledni prvek
	- i - prvni prvek
	- j - posledni prvek (1 pred pivotem)
- Chci:
	- vlevo mit prvky mensi nez pivot
	- vpravo mit prvky vetsi nez pivot
- V cyklu se divam na hodnoty na indexu i a j:
	1. Obe jsou spatne - prohodim
	2. Vlevo je v poradku, vpravo je spatne - inkrementuju levy index
	3. Vpravo je v poradku, vlevo je spatne - inkrementuju pravy index
	4. Oba jsou spravne - posun obou indexu
	-  Tohle provadim dokud se i a j nepotkaji
		- Tento proces se jmenuje neutralizace
		- V kazde iteraci je neutralizovan nejmene jeden prvek
	- Nakonci prohodim pivota s prvkem na indexu j (aby byl pivot spravne)

Paralelizace:
- Mame globalni promennou i a j
- Kazde vlakno si vezme sve vlastni i a j a inkrementuje/dekrementuje globalni hodnotu
	- Tohle by vedlo na hodne velkou rezii
	- -> Kazde vlakno si vezme i+k a j-k a neutralizuje tyto segmenty
		- Kazdy segment je vzdy bud neutralizovat nebo spinavy
		- Pokud mame neutralizujeme 2 segmenty, pak bereme nove segmenty z obou stran
		- Pokud mame 1 spinavy, pak bereme segment jen z ciste strany a docistime druhy segment
- Na zaver nam zustane maximalne p spinavych segmentu, ktere sekvencne vycistime
## Merge Sort
Sekvencni kod: ![[Pasted image 20240602200108.png]]

Potrebujeme:
- merge - vezme setridene pole a mergne je do sebe, tak aby byly setridene
- mergesort_rec - rozdeli rekurzivne pole na poloviny a na zaver merguje pomoci merge
- mergesort - vytvori pomocne pole a spusti rekurzi