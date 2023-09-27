Single responsibility principle
	- Trida dela jen jednu vec
Open-closed principle
	- Trida je otevrena pro rozsiritelnost
	- Trida je zavrena pro modifikace
Liskov Substitution Principle
	- Na pozici predka je mozne dosadit potomka a melo by to porad fungovat
	- vetsinou zajisteno jazykem
Interface Segregation
	- Rozdeleni interfacu na mensi celky
	- Interface na CRUD muzeme rozdelit na 4 interfacy:
		- C, R, U, D
		- Pak muzu implementovat jen to co je potreba
Dependency Inversion
	- Nejsme zavisli na konkretni implementaci
	- Injektujeme interface