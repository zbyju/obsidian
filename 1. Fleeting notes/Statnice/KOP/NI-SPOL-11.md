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
=> PI je alespon tak tezky jako vsechny z X
=> PI muze byt tezsi nez vsechny z X

Problem PI je X-complete, jestlize je X-hard a zaroven patri do X.
=> PI je alespon tak tezky jako vsechny z X
=> PI je nanejvys tak tezky jako vsechny z X
## Redukce
1. Instance problemu PI1
2. Prevod
3. Instance problemu PI2
4. Algoritmus na reseni PI2
5. Shodny vystup
=> Mame algoritmus na PI1, ktery neni horsi nez PI2
=> PI1 je nejvys tak tezky jako PI2
=> PI2 je nejmene tak tezky jako PI1
### Karpova Redukce
Algoritmus ktery na DTS prevede instanci PI1 na instanci PI2 v polynomialnim case a vystup obou instanci je stejny.

Pokud je PI1 karp-redukovatelny PI2 a naopak, pak jsou polynomialne ekvivaltentni.

Karp redukce je tranzitivni
# NP-Hard a NP-Complete
Problem PI je NP-hard, jestlize pro vsechny problemy $\Pi' \in NP, \Pi'\ <karp>\ PI$
= pokud jsou na nej prevoditelne vsechny problemy z NP

Problem PI je NP-complete, pokud je z NP a je NP-hard

![[Pasted image 20240530000450.png]]

Dokazat ze nejaky problem je NPC se da tak ze nalezneme redukci nejakeho problemu z NPC (treba SAT) na nas problem v polynomialnim case.
## Cookova veta
SAT je NP-complete
## NPO
Optimalizacni problem PI je NPO, jestlize:
- velikost vstupu lze zapsat v polynomialnim case
- kontrola reseni patri do P
- kontrola optimalizacniho kriteria patri do P
## PO
Optimalizacni problem PI je NPO, jestlize:
- Patri do NPO
- Existuje program pro DTS, ktery kazdou instanci vyresi v polynomialnim case.
## Turingova Redukce
Problem PI1 je Turing redukovatelny na PI2, jestlize existuje algoritmus pro DTS, ktery resi kazdou instanci problemu PI1 tak, ze pouziva program M2 pro problem PI2 jako podprogram (jehoz trvani povazujeme jako jeden krok).

(redukce nemusi obecne nemusi probehnout v polynomialnim case)

Problem PI je NP-hard, jestlize pro vsechny problemy z NP existuje turingova redukce v polynomialnim case na problem PI

Karpova redukce je specialnim pripadem Turingovy redukce v polynomialnim case
- => volani podprogramu pouze jednou, prime pouziti vysledku
- => $NPC \subset NPH$
## NPI
NPI = NP - P - NPC
# Pseudopolynomialni problem
Problem ktery polynomialne zavisi na velikosti instance, ale take na vstupni promenne, ktery s velikosti instance nesouvisi
(omezeni na max vahu batohu se da zvysovat hodne)
# Relativni chyba a kvalita
C(S) - hodnota optimalizacniho kriteria
APR(I) - aproximovane reseni instance I
OPT(I) - optimalni reseni instance I

## Relativni Kvalita R
### $R \geq max_{\forall I} \{\frac{C(APR(I))}{C(OPT(I))},\frac{C(OPT(I))}{C(APR(I))}\}$
## Relativni Chyba $\epsilon$
### $\epsilon \geq max_{\forall I} \frac{|C(APR(I)) - C(OPT(I))}{max\{C(OPT(I)), C(APR(I))\}}$
## Aproximativni algoritmus
Algoritmus APR pro problem PI je R-aproximativni ($\epsilon$-aproximativni) pokud kazdou instanci vyresi v polynomialnim case s relativni kvalitou R (relativni chybou $\epsilon$)

Optimalizacni problem PI je R-aproximativni pokud pro nej existuje R-aproximativni algoritmus. Cislo R nazveme aproximacnim prahem.

Optimalizacni problem PI patri do tridy APX, jestli ze je R-aproximativni s konecnym R.
### PTAS
Algoritmus APR, ktery pro kazde $1 \gt \epsilon \gt 0$ vyresi instanci I problemu PI s relativni chybou nejvyse $\epsilon$ v polynomialnim case nazyvame polynomialni aproximacni schema problemu PI.

Problem PI patri do PTAS pokud pro PI existuje polynomialni aproximacni schema.
### FPTAS
Polynomialni aproximacni schema APR, jehoz cas vypoctu zavisi polynomialne na $1/\epsilon$ nazyvame plne polynomialni aproximacni schema.

Problem PI patri do FPTAS jestlize pro nej eixstuje FPTAS algoritmus. 

![[Pasted image 20240530172856.png]]
