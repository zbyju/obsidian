**Princip simulovaného ochlazování, význam parametrů a způsoby jejich řízení.**

# Simulovane Ochlazovani
Heuristika, ktera funguje na mechanismu diverzifikace a intensifikace.

Ma nekolik ridicich parametru a procedur:
- Teplota
	- $\delta$ = how_much_worse
	- probability prijeti noveho stavu = $exp(- \frac{\delta}{T})$
	- jinak zustan ve stavajicim stavu
- Pocatecni teplota

- try
	- vrat dalsi stav, ktery mam zkusit
- how_much_worse()
	- vyhodnot jak moc je novy stav horsi nez stavajici
	- Minimalizacni problem:
		- novy cost - stavajici cost
	- Maximalizacni cost:
		- stavajici cost - novy cost
- frozen()
	- uz to zmrzlo a nema cenu se koukat dal
- equilibrium()
	- uz jsem nasel ustalene reseni
	- pocet akci N
	- N prijatych akci nebo 2N akci
- cool()
	- vypocet nove teploty
	- $\frac{c}{log(1+k)}$ - prilis pomale
	- $\alpha \cdot T$ - kde $\alpha$ nekde mezi 0.8 a 0.999

Dale musime urcit nalezitosti ktere jsou obecne pro problemy stavoveho prostoru:
- Stavy
- Operatory
- Omezujici podminky
- Pocatecni reseni

Stavovy prostor ma byt symetricky = vygenerovani akce $a$ a $a^{-1}$ by melo mit stejnou pravdepodobnost.

## Vyber parametru
### Vstup
Pokud ma instance prevynasobeny vstup 100, pak bychom meli operovat s teplotou\*100.

Reseni:
Normalizace
	- Vstup upravime tak aby byl v range 0-1
### Pocatecni teplota
Nastavime tak aby prijeti prvni zhorsujici akce pravdepodobne.
"Pravdepodobne" - dalsi parametr, obvykle treba 0.5

1. Rychle zvysujeme teplotu a sledujeme cetnost prijatych zmen k horsimu
2. Nastavime teplotu na tu ktera mela vhodny pomer
3. Nastavime puvodni pocatecni stav
4. Spustime s teplotou
## Pocatecni stav
Zacit v reseni a pohybovat se ve stavu reseni:
- zvolit nahodne pocatecni reseni
	- moznost restartu v nahodnem jinem pocatecnim reseni
- konstrukce pocatecniho reseni
	- zkonstruuji nejake pocatecni reseni (netrivilani)
## Problemy
- Mala pocatecni teplota
	- => stavovy prostor se prilis neprozkouma a vysledek bude blizky pocatecnimu reseni
- Vysoka pocatecni teplota
	- => zbytecne dlouhy vypocet
- Brzke ukonceni
	- => nedojde k intensifikaci a nenajde se lokalni optimum
- Pozdni ukonceni
	- => zbytecne zlepsujeme marginalne
