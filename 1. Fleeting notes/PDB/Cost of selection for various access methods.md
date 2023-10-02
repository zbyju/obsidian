select * from R where A = 'x'

**no index**
full table scan
cost = pR/2 pokud unikatni
cost = pR pokud neni unikatni

**unique index on R(A)**
cena = hloubka indexoveho stromu + 1 pro skok pres rowid do bazove databaze
