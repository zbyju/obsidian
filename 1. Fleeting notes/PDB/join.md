Mam relaci R(a, ...), S(k, a, ...)
a je klic R; k je klic S, a maji spolecne

zajima nas cena I/O blocku
porovnani jednotlivych radku je 0

algoritmy:

**nested loop join**:
foreach pres R
	foreach pres S
		najdi spojitelne zaznamy a dej je na vystup

Podle velikosti memory tak zalezi jak moc bude moct byt nacteno do pameti

**merge join**:
sortnu R podle a
sortnu S podle a
mergnu sestridene

**hash join**:
vezmeme hash funkci (mod(k))
aplikuju hash funkci na obe relace
zmensuje to pocet vzajemnych provnani

**nested loop join**: