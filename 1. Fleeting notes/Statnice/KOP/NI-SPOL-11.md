**Význam tříd NP a NPH pro praktické výpočty.**

# Problem a Instance
Problem = Obecna formulace
Instance = Konkretni instance problemu

(Similar to class vs object)
# Charakterizace Problemu
- Vstupni promenne
	- Vstup
- Vystupni promenne
	- Vystup
- Konfiguracni promenne
	- To co nastavuje hruba sila
	- To na cem se daji zkontrolovat omezeni
	- Pro nejake tridy problemu se shoduji s vystupnimi
- Omezeni
	- Dalsi omezeni pro problem, ktere musi byt splneny
- Optimalizacni kriterium (optional)
## Charakterizace Instance
- Ohodnoceni vstupnich promennych
### Konfigurace
Ohodnoceni konfiguracnich promennych
### Reseni
Konfigurace ktera vyhovuje omezujicim podminkam
### Optimalni Reseni
Reseni s nejlepsi hodnotou optimalizacniho kriteria
### Suboptimalni Reseni
Reseni ktere ma ”prijatelnou hodnotu” optimalizacniho kriteria
## Verze Problemu
Problemy se deli na ruzne verze. Tyto verze maji stejny vstup a konfiguracni problemy (s vyjimkou konstanty), omezeni. Lisi se pouze ve vystupu.
### Bez optimalizacniho kriteria
- Rozhodovaci problem
	- Existuje Y takove, ze R(I, Y)? Ano/Ne
	- Plati pro vsechna Y, ze R(I, Y)? Ano/Ne
- Konstruktivni problem
	- Sestroj nejake reseni Y, ze R(I, Y) Y
- Enumeracni problem
	- Sestroj vsechna reseni Y, ze R(I, Y) {Y}
- Pocetni problem
	- Kolik je Y, ze R(I,Y) $m \in \mathbb{N}$
### S optimalizacnim kriteriem
- Optimalizacni konstruktivni problem
	- Sestroj nejake Y, ze R(I, Y) a C(Y) je nejlepsi mozne
- Optimalizacni evaluacni problem
	- Zjisti nejlepsi mozne C(Y), ze R(I,Y)
- Optimalizacni rozhodovaci problem
	- Existuje Y, ze R(I, Y) a C(Y) je alespon tak dobre jako konstanta K?
- Optimalizacni pocetni problem
	- Kolike je Y takovych, ze R(I,Y) a C(Y) je aspon tak dobre jako konstanta K?
- Optimalizacni enumeracni problem
	- Sestroj vsechna Y, ze R(I, Y) a C(Y) je nejlepsi mozne

## Vypocetni modely
### Turinguv stroj
- Mnozina symbolu pasky (soucast je b - blank) P
- Mnozina symbolu vstupu (soucasti nesmi byt b) V
- Mnozina stavu (q0 - pocatecni)
- Koncove stavy $q_{ano},q_{ne}$ 
- Vypocet: $(q \in Q, s \in P) \rightarrow (q', s', \Delta)$ (stav, cteny symbol) -> (novy stav, zapsany symbol, pohyb hlavy)
#### Nedeterministicky Turniguv stroj
Muzeme si predstavit pomoci:
- Klonovani
	- V kazdem kroku se naklonuje pro vsechny budouci stavy
	- Jeden z klonu najde reseni a oznami ostatnim
- Vsevedouci napoveda
	- V kazdem kroku si vybere tu "spravnou" moznost pro nasledujici stav
Resi NP problem tak, ze vysledna cesta k reseni je "unosne dlouha".

Turinguv stroj:
- **resi rozhodovaci problem PI**, pokud se vypocet zastavi po konecnem poctu kroku pro kazdou instanci problemu PI
- **resi rozhodovaci problem PI v case t**, pokud se vypocet zastavi po nejvice t krocich pro kazdou instanci PI
- **resi rozhodovaci problem PI s pameti m**, jestlize kazda instance je vyresena se zaplnenim maximalne m policek
Nedeterministicky TS:
- **resi rozhodovaci problem PI v case t**, pokud se vypocet zastavi po t krocich pro kazdou instanci, **ktera ma za vysledek ANO**.
### RAM stroj
Schopny adresovat
### Booleuv obvod
Formalizovana sit hradel
# Trida P
Rozhodovaci problem patri do tridy P, jestlize pro nej existuje program pro DTS, ktery jej **resi v polynomialnim case** = $O(n^k)$; kde n = velikost instance, k = konecne cislo.

Staci aby existoval nemusime o nem vedet.
## PSPACE
Rozhodovaci problem patri do PSPACE, pokud existuje program pro DTS, ktery jej resi v polynomialni pameti = $O(n^k)$
## EXPTIME
Rozhodovaci problem patri do PSPACE, pokud existuje program pro DTS, ktery jej resi v polynomialnim case = $O(2^{P(n)})$; kde P(n) je polynom ve velikosti instance
# Trida NP
Rozhodovaci problem patri do tridy NP, jestlize pro nej existuje algoritmus na **NTS**, ktery resi vsechny instance, ktere maji **reseni ANO**, v polynomialnim case $O(n^k)$; n = delka vstupnich dat, k = konecne cislo.

Ekvivalentni definice pomoci certifikatu:
Rozhodovaci problem patri do tridy NP, jestlize pro kazdou instanci problemu, ktera ma **reseni ANO**, **existuje konfigurace Y takova, ze kontrola, jestli Y je reseni patri do P.**
=> Pak Y je svedek = certifikat.

=> pro overeni jestli je problem v NP staci overit, jestli kontrola reseni se da udelat v P case.

### => $P \subseteq NP$

# Komplementarni Problemy
Mejme problem PI, ktery obsahuje vsechny instance, ktere maji vystup ANO
Pak komplement k PI je definovan jako doplnek k teto mnozine.

Mejme NP problem $\exists Y, R(I, Y)$ => coNP problem: $\forall Y, not R(I, Y)$
- Vstupni probmenne zustanou stejne

NP Problem:
- ma kratke svedky pro instance ANO
- nema kratke svedky pro NE
co-NP Problem:
- nema kratke svedky pro ANO
	- vracim hodne svedku ktere se daji kratce overit ale je jich hodne
- ma kratke svedky pro NE (protipriklad)

P = co-P
![[Pasted image 20240529222849.png]]
# X-Hard X-Complete
Efektivni reseni = v polynomialnim case, nebo s omezenou chybou
zredukovat na reseni PI = vyresit pomoci nejakeho resice pro PI

Problem PI je X-hard, jestlize se efektivni reseni vsech problemu z tridy X da zredukovat na efektivni reseni problemu PI.
=> resic pro PI muze slouzit jako efektivni resic vsech problemu X

Problem PI je X-complete, jestlize je X-hard a zaroven patri do X.
## Redukce