**Význam tříd NP a NPH pro praktické výpočty.**

# Problem
Obecna formulace
# Instance
Konkretni instance problemu
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

# Charakterizace Instance
- Ohodnoceni vstupnich promennych

## Konfigurace
Ohodnoceni konfiguracnich promennych

## Reseni
Konfigurace ktera vyhovuje omezujicim podminkam

## Optimalni Reseni
Reseni s nejlepsi hodnotou optimalizacniho kriteria

## Suboptimalni Reseni
Reseni ktere ma ”prijatelnou hodnotu” optimalizacniho kriteria

# Verze Problemu
Problemy se deli na ruzne verze. Tyto verze maji stejny vstup a konfiguracni problemy (s vyjimkou konstanty), omezeni. Lisi se pouze ve vystupu.
## Bez optimalizacniho kriteria
- Rozhodovaci problem
	- Existuje Y takove, ze R(I, Y)? Ano/Ne
	- Plati pro vsechna Y, ze R(I, Y)? Ano/Ne
- Konstruktivni problem
	- Sestroj nejake reseni Y, ze R(I, Y) Y
- Enumeracni problem
	- Sestroj vsechna reseni Y, ze R(I, Y) {Y}
- Pocetni problem
	- Kolik je Y, ze R(I,Y) $m \in \mathbb{N}$
## S optimalizacnim kriteriem
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

# Vypocetni modely
## Turinguv stroj
- Mnozina symbolu pasky (soucast je b - blank) P
- Mnozina symbolu vstupu (soucasti nesmi byt b) V
- Mnozina stavu (q0 - pocatecni)
- Koncove stavy $q_{ano},q_{ne}$ 
- Vypocet: $(q \in Q, s \in P) \rightarrow (q', s', \Delta)$ (stav, cteny symbol) -> (novy stav, zapsany symbol, pohyb hlavy)

Turinguv stroj:
- **resi rozhodovaci problem PI**, pokud se vypocet zastavi po konecnem poctu kroku pro kazdou instanci problemu PI
- **resi rozhodovaci problem PI v case t**, pokud se vypocet zastavi po nejvice t krocich

## RAM stroj
## Booleuv obvod