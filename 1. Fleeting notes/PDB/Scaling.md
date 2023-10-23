schopnost systemu zvladat odbavovat pozadavky pri zvysujicim se poctu dat / queries

### vertical scaling
(scaling up/down)
pridame nejakou komponentu - zvysime pocet CPU, koupime lepsi stroj, zvysime pamet

vsechny stroje maji nejaky limit
je to drahy
spatne se predikuje co bude potrebovat
vendor lock
nekdy se to hodi

### horizontal scaling
(scaling out/in)

pridavame vice nodu do systemu

often no single point of failure
vyrazne zvysuje komplexitu system
	- i z pohledu managementu
	- i z pohledu programovani
dost casto mame spatne predpoklady:
	- sit ma vypadky
	- latency neni 0
	- nemame neomezenou propustnost site
	- topologie se muze menit
	- sit neni homogonni
	- prenost dat neni za 0 
muze byt slozite rozdelit databazi pres vice nodu, tak aby se zachovala efektivita