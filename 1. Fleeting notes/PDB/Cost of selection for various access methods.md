select * from R where A = 'x'

**no index**
full table scan
cost = pR/2 pokud unikatni
cost = pR pokud neni unikatni

**unique index on R(A)**
cena = hloubka indexoveho stromu + 1 pro skok pres rowid do bazove databaze
cena = hloubka indexoveho stromu pokud mame indexem organizovanou tabulku

**non-unique index on R(A)**
cost = hloubka indexoveho stromu + pocet bloku s hodnotou A = 'x'

select B from R where A = 'x'

**compose index on R(A)** non-unique
cost = hloubka stromu + (pocet bloku A='x' / block factorem indexu )
neni potreba vubec sahat do bazove tabulky

**compose index on R(A)**
cost = hloubka stromu

select A from R where A < 'x';

**index query only**
najdu bod A ='x' pak vezmu vsechno vlevo (v listech)

**base table query**