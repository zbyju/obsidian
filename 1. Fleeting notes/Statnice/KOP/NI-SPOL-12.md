**Experimentální vyhodnocení algoritmů, zejména randomizovaných.**

# Experiment
- Otazka
- Plan
- Provedeni
- Sber data
- Interpretace
- Odpoved
- Znovu
# Metrika
Merime ruzne metriky, ktere nas zajimaji:
- Vstupni
	- velikost vstupu
- Vystupni
	- Slozitost
Pri vyhodnocovani se snazime drzet vstupni metriky konstantni, menit jen treba jednu promennou a sledovat vystupni metriky.

## Distribucni funkce
x - pocet kroku algoritmu
y - pravdepodobnost ze algoritmus skoncil po danem poctu kroku
(na resitelnych instancich)

+muzeme pronasobit uspesnosti v danem kroku (pravdepodobnost ze algoritmus **uspesne** skoncil v danem kroku)

## Randomizovany algoritmus
2 zdroje variance -> dva stupne zpracovani
- Vstupni variance = performance rozdily, ktere jsou zapricenene rozdily vstupnich dat
- Internal variance = performance rozdily zapricenene randomizovanym vypoctem

We use 2 levels of statistics to interpret the results to account for both sources of variance.

### Metriky 1. stupne
Snazi se o potlaceni vstupni randomizace

- Charakteristika rozlozeni
	- Average
	- Median
	- Variance
	- Range
	- Skewness
- Dominance
	- Jak casto je algoritmus lepsi nez jiny algoritmus
	- Domination matrix
	- Win ratio
	- Average rank
	- Pairwise comparison
	- Omezeni na urcite typy instanci (jen velke instance, jen male, ...)
- Uspesnost do urciteho poctu kroku
	- Distribucni funkce

### Robustnost Heuristiky
Cistlivost vykonu algoritmu na popis/zapsani instance.

Algoritmus muze mit lepsi vysledky pokud je ten stejny vstup zapsan jinak (jine poradi)

Muzeme testovat pomoci prehazeni deklaraci mnozin = perturbace
### Generovani vstupu
- Zcela nahodne
- Nejake specificke

Nebo pokud chceme vic realisticke vstupy musime pouzit standardni sady - predpriveny set instanci.
-> vysledek je pak relevantni (pouze) k te sade
## Evaluation
1. White box evaluation
	- Sledujeme jak algoritmus pracuje
	- Menime parametry
2. Black box evaluation
	- Delame po white box evaluation
	- Finalni vyhodnoceni na zvolenych metrikach
# Randomizovane algoritmy
Zalozen na nahodne volbe

Jsou jednoduche, robustni
## Monte carlo
Dosazeny vysledek je nahodna promenna; cas behu pevny pro danou instanci.

Z herny se dostanu rano, ale nevim kolik jeste budu mit penez
## Las Vegas
Cas behu je nahodna promenna, vysledek je vzdy spravny

Z herny se dostanu s 0 penezi, ale nevim kdy