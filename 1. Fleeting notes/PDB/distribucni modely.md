sharding
ruzne data na ruznych nodech
rozdelime data a davame je na ruzne nody

replication
stejne data na ruznych nodech

muzeme pristupy kombinovat

nosql s tim vice pocitaji


### sharding
treba v mongu to znamena ze jednu kolekci na jednom uzlu, druhou na druhem, ale dokaze treba distribuovat data rovnomerne mezi uzly

cil je udelat to tak aby se co nejmene museli dotazovat pres vice uzlu

mapovani dat muzeme delat na zaklade ruznych strategii
round robin
EU data v EU databazi
apod.

### replikace
stejny data na ruznych uzlech
replikacni faktor (kolik kopii od jednoho data mam)

**master-slave**
master neco udela
slavove jen followuji
muzeme cist z slavu i mastera
dobre pokud uzkym hrdlem bylo cteni
read intensive aplikace
pri vypadku mastera se nemuze zapisovat
pak jsou ruzne strategie pro zvoleni noveho mastera

write-read conflict problem - na masteru zapsano, na slavovi jeste ne
write-write conflict - neni

**peer-to-peer**
vsichni jsou masteri, vsichni replikujou
problemy s konzistenci (tohle zmen, tohle zmen na jinych uzlech ve stejny moment)
^ write-write conflict
read-write conflict tady taky muzeme nastat (na jednom zapisu, na druhem ctu jeste stare data)

### kombinace sharding + replication
neni potreba mit replication factor stejny jako pocet nodu
neni potreba zajistovat ze se data replikuji do vsech nodu, kde maji byt
