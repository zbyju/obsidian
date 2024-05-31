**Princip lokálních heuristik, pojem globálního a lokálního minima, obrana před uváznutím v lokálním minimu.**

# Lokalni metoda
Divame se na aktualni konfiguraci (jednu) a vybirame pristi konfiguraci z jejich sousedu.
## Stav
Algoritmus/system je black-box, na stejny vstup reaguje jinak; informace ktera urcuje jak bude reagovat = stav.

Pro kombinatoricke problemy jsou to vsechny hodnoty ktere ovlivnuji chod algoritmu.
## Stavovy prostor
Mame X={x1, x2, ..., xn} konfiguracni promenne problemu PI; dale mame Z={z1, z2, ..., zn} - vnitrni promenne algoritmu $A$ resiciho instanci I problemu PI. Kazde ohodnoceni promennych $X \cup Z$ je stav algoritmu A resiciho I.

S={s1, s2, ..., sn} je mnozina stavu algoritmu A resiciho I a Q={q1, q2, ..., qn} je mnozina operatoru S->S takovych, ze qi(si) != si pro vsechna qi a si. Pak dvojice (S, Q) je stavovy prostor algoritmu A resiciho I.
## Akce
s z S (s je konkretni stav z S) a q operator z Q, pak aplikace q na s (q(s)=s') je **akce** nebo tah.
## Graf stavoveho prostoru
Necht (S, Q) je stavovy prostor, pak orientovany graf H=(S, E) kde hrany jsou (si, sj) pokud existuje akce qk(si)=sj pro nejaky operator qk. H nazveme grafem stavoveho prostoru algoritmu.
### Okoli stavu, sousedni stav
Okoli stavu s z S je mnozina stavu dosazitelnych z s aplikaci nektereho operatoru. Stavy z okoli stavu s jsou sousedni stavy.
### k-okoli stavu
Mnozina stavu dosazitelnych aplikaci 1 az k operaci.
### Vlastnosti grafu stavoveho prostoru
Volbou operatoru menime vlastnosti stavoveho prostoru:
- Acyklicky 
	- Omezena delka cesty
	- Jednoduche rizeni algoritmu
	- Typicky pro hladove algoritmy
- Cyklicky
	- Komplikovanejsi rizeni
	- Pokrocile heuristiky
### Dostupnost
(S, Q) stavovy prostor, H=(S,E) jeho graf. Pro kazde dva stavy si, sj z S nazveme delku nejkratsi cesty z si do sj v grafu H jako (orientovanou) vzdalenost uzlu sj od si.

Graf je dostupny pokud mezi kazdymi dvema uzly existuje cesta (graf je silne souvisly)

Graf je symetricky pokud pro kazde dva stavy si, sj z S je vzdalenost sj od si priblizne stejna jako si od sj.
# Strategie prohledavani
Mejme stavovy prostor (S, Q), pak strategii myslime jakym zpusobem ridit pohyb (aplikace q) na zaklade aktualniho stavu.
## Uplna strategie
Navstivi vsechny stavy krome tech o kterych vime ze nemaji optimalni reseni.
## Systematicka strategie
Uplna strategie, ktera navstivi kazdy stav maximalne jednou.
## Uplny algoritmus
Dokaze odpovedet, ze instance nema reseni

Nemusi to byt lokalni heuristika; ale pouziti uplne strategie v lokalni heuristice nam da uplny algoritmus
## Branch&Bound
Metoda prorezavani, kde za pomoci omezujiciho a optimalizacniho kriteria orezavame vetve prostoru, kdyz vime ze vetev neobsahuje reseni, nebo je reseni horsi nez jiz nalezene reseni.
# Lokalni optimum
Jednoduche lokalni heuristiky skonci v lokalnim optimu a tam skonci.

Heuristiku muzeme zkouset spoustet z ruznych pocatecnich stavu, abychom ziskali lepsi reseni. Tohle je ale je spis naivni fix, ktery neni moc robustni.
Chceme algoritmus ktery je schopen pripustit horsi stav, ale stale hleda optimum.

Pouzivame 2 strategie: diverzifikace, intenzifikace pri vypoctu.
## Diverzifikace
Velka ochota udelat akci, ktera vede do horsiho stavu

=> vede na rovnomerny pruzkum stavoveho prostoru (vlastne bez cile)
## Intenzifikace
Mala ochota udelat akci, ktera vede do horsiho stavu

=> Konvergence k finalnimu nejlepsimu reseni
