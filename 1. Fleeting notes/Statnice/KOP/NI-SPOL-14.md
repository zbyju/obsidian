**Princip genetických algoritmů, význam selekčního tlaku pro jejich funkci.**

# Simulovana Evoluce
Pracujeme s vice stavy najednou
- Snizeni uvaznuti v jedinem optimu

Operator SxS->S nebo SxS->SxS

1. Pocatecni populace
2. Selekce
	- Zvyseni podilu zdatnych jedincu
3. Krizeni
	- Rekombinace geneticke informace do novych jedincu
4. Mutace
	- Nahodny zdroj nove geneticke informace
5. Znovu selekce
6. => Konecna populace

Spolecne rysy:
- Vice stavu (jedincu, individui)
- Interakce stavu
	-  Novy stav je kombinace reprezentaci
- Diverzifikace pomoci mutace
- Intenzifikace pomoci selekce
	- Selekce pro kombinaci
	- Selekce pro dalsi generaci
Rysy jednotlivych algoritmu:
- Vyber reprezentace
- Vyber unarnich a binarnich operatoru
- Vyber selekce pro konstrukci nasledujici generace
- Vyber strategie krizeni
Caste volby:
![[Pasted image 20240531214329.png]]
![[Pasted image 20240531215621.png]]
## Generace
### $\mu + \lambda$ potomku
Mejme $\mu$ individui (rodicu), ktere vyprodukuji dohromady $\lambda$ individui (potomku) + $\mu$ individui pro pokracovani
Z nich se vybira $\mu$ individui, ktere pokracuji ($\mu + \lambda$ strategie)

Vyber z individui:
- Nahrada (en bloc): $\lambda = \mu$
	- nova generace nahradi puvodni
- Nahrada s elitismem
	- ponechame par nejlepsich elitnich jedincu a zbytek novy
- Soutez
	- z $\mu + \lambda$ individui udelame soutez a vybereme $\mu$ novych
#### Specialni pripady
$\mu = 1; \lambda = 1$ - jednoduche heuristiky (1 jedinec, z okoli vyberu jedno a nahradim)
$\mu = 1; \lambda > 1$ - zacleneni noveho individua = steady-state strategie

## Geneticke Algoritmy
### Kodovani
- Binarni retez
	- Klasicka formulace
	- Teoreticky vzdy mozne
	- Prirozeny pro radu problemu (SAT)
- Vektor promennych
- Permutace retezce z dane abecedy
### Rizeni operatoru
Volime pravdepodobnosti pro:
- Krizeni
	- default 1
- Mutaci
	- default 0.03
### Krizeni
- Jednobodove krizeni
	- Zvolime nahodny bod
	- Vysledek ziskame spojenim leve casti jednoho kodovani s pravou casti druheho
- Dvoubodove krizeni
	- Zvolime dva body
	- Vysledek ziskame spojenim "kraju" jednoho kodovani s "prostredkem" druheho 
	- ![[Pasted image 20240531220417.png]]
- Uniformni krizeni
	- Kazdy "bit" bereme nahodne bud z jednoho nebo druheho jedince
- Permutacni krizeni
	- Potrebujeme krizeni, ktere ma za vysledek permutaci
	- ![[Pasted image 20240531220637.png]]
	- Dva body kde mam hodnoty z kterych udelam mapovani
- Inverze
	- Problem jedno a dvou bodovych krizeni je ze je zavisle na poradi genu
		- Bit na konci prvniho genu ma v pripade jednobodoveho krizeni velmi nizkou sanci ze tam zustane
	- Reseni je prochazet poradi bitu (ale zanechat vyznam promennych)
		- Pak je mozne to zase vratit zpet, tak aby poradi promennych bylo spravne
### Mutace
- Klasicke mutovani
	- Dam si vsechny jedince vedle sebe
	- Vyberu x bitu ktere zmenim
		- Bity jsou voleny nahodne jednou pro celou generaci
		- Muze se stat ze nejaky jedinec nebude mutovan vubec, nebo nejaky nekolikrat
### Selekce
Chceme aby pocetni zastoupeni jedince v populaci odpovidalo jeho zdatnosti
=> Prevod informace zdatnosti na informaci cetnosti
=> Vyber durazu na zdatnost jedince
=> Hlavni nastroj pro vyvazeni diverzifikace a intenzifikace

Hodnota kontrolujici prevod/prepocet je **selekcni tlak**.
#### Selekcni tlak
Pravdepodobnost vyber nejlepsiho jedince

Extremy:
p = 1: intenzifikace
p = 1/n: nezalezi na zdatnosti, diverzifikace
#### Vyvazeni
Je potreba vyvazit sum pochazejici z mutace a selekcni tlak.

Pokud je sum moc vysoky
- random walk
Pokud je velky selekcni tlak
- duraz na konvergenci
- nebezpeci degenerace populace (lokalni optima)
Pokud je maly selekcni tlak
- Pomala konvergence
- Sum prevlada -> divergence

Snizujeme-li selekcni tlak, je mozna zapotrebi snizit i pravdepodobnost mutace.
### Nahodny vyber selekce
- Ruletovy vyber
	- ![[Pasted image 20240531230111.png]]
	- Provedeme m nahodnych voleb uhlu => m prvku
	- Jeden prvek muze byt vybran vicekrat
	- Prvek nemusi byt vybran vuber
- Univerzalni stochasticke vzorkovani
	- Vyberu pouze jeden uhel
	- Nasledne vyberu m-1 rovnomerne rozmistenych dalsich
		- k prvnimu uhlu postupne pricitam $2\pi / m$
	- ![[Pasted image 20240531230425.png]]

#### Rizeni selekcniho tlaku s ruletou
Vybrali jsme si ruletovy vyber. Vypocet selekcniho tlaku (pravdepodobnosti vyberu nejlepsiho):
- Prima umera
	- Udelame primou umeru mezi zdatnosti a pomernou pravdepodobnosti vyskytu
	- Casto degeneruje
- Scaling
	- Prepocitani zdatnosti linearni funkci
	- ![[Pasted image 20240531230847.png]]
	- Vyberu nejake Z1, Z2
	- Naskaluju nejlepsiho na Z2
	- Nasklauju nejhorsiho na Z1
	- Zbytek pomerne taky
	- => zezacatku muze snizovat rozdily (=> vetsi diverzifikace)
	- => ke konci behu zvysuje rozdily (=> vetsi intenzifikace)
- Ranking
	- Pouziti poradi ve zdatnosti misto zdatnosti samotne
	- Seradim si jedince podle zdatnosti
	- Skaluji linearne jejich poradi
	- ![[Pasted image 20240531231345.png]]
- Truncation selection
	- Prahovani, zkraceny vyber
	- Vyberu castu jedincu, zbytek zahodim
	- Pak je nahodne mezi sebou mnozim
- Turnajovy vyber
	- Nahodne vyberu r jedincu
		- = turnaj
		- z teto podmnoziny vyberu nejlepsiho
	- Opakuju dokud nenaplnim populaci
	- Selekcni tlak se ridi velikosti turnaje
		- r = n => p = 1 => intenzifikace
		- r = 1 => p = 1/n => diverzifikace
### Generace
#### Rizeni
- Nahrada
	- Nahrada cele generace za novou
- Nahrada s elitismem
	- Vybereme x nejlepsich, ty nechame
	- Zbytek nahradime za novou
	- Vede na degeneraci

Velikost populace:
- Chceme velkou, ale to zvysuje overhead
- Cim slozitejsi je vyhodnoceni optimalizacniho kriteria tim mensi populaci
- Velikost populace muzeme linearne zvetsit s velikosti instance
	- + omezeni
### Podminky ukonceni
- Pevny pocet generaci
- Priznaky konvergence
	- Zmena prumerne zdatnosti
	- Rozlozeni zdatnosti v generaci
### Omezujici podminky
Co delat, kdyz jednotlivec nesplnuje omezujici podminky
- trest smrti
	- zahodit pokud nesplnuje
- oprava
	- muze vnaset nejaky bias
	- jakym smerem to opravi
- relaxace
	- promitneme do zdatnosti
	- nejlepe pokud umime vyhodnotit jak moc porusujeme podminku
- domenova reprezentace
	- pouzivame reprezentace nebo operatory, ktere vedou jen na platne reprezentace
- dekodery
	- mame reprezentaci
	- + mame dekoder ktery z jakekoliv reprezentace vyrobi reseni
		- mel by byt fer
		- mel by byt schopen dat jakekoliv reseni
		- dodrzovat lokalitu
			- mala zmena v reprezentaci => mala zmena reseni
		- rychly vypocet
	