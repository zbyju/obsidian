Tabulka je organizovana po blocich
U heap table:
- Pocet radku
- \#R[A] - Pocet hodnot A v relaci R, kdyz si vyberu sloupec, kolik je tam ruznych hodnot
- pR - \# pages to store R - pocet radku ktere v prumeru se vlezou do bloku
- bR - block factor

B strom:
- f(A, R) - faktor vetveni, prumerny pocet children
- I(A, R) - hloubka indexoveho stromu
- p(A, R) - pocet listovych bloku v indexovem stromu

Pridavne statistiky:
- min, max values
- histogramy - je to pomoc pro optimalizator

Index statistics
- Clustering factor
	- Pocet datovych bloku, ktere je potreba navstivit abychom dostali setridene data podle indexu
	- Jak hodne jsou hodnoty v bazove tabulce rozhazene vuci klici - indexu
	- V b stromu jsou rowid pointery do bazove tabulky, v b stromu jsou setridene, ale v bazove tabulce setridene nejsou
	- min hodnota pocet bloku
	- max hodnota pocet radku

Clustered index - index pres tabulku setrideny podle index klice
Composed key index - 
Reverse index - cislo ze sekvence pro index se bere odzadu aby kdyz se vklada do B stromu, tak aby ho to nevyvazovalo, ale takhle se tam bude vkladat na jednu stranu a pak na druhou 

#