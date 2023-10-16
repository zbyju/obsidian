Dokumentova databaze

Jednotka = JSON document
Kazdy dokument ma id (\_id)

max size 16kb
gridfs pro vetsi

primary key - unique, immutable, muze byt jakehokoliv typu krome array, nemel by to byt autoinkrement, pouziva se UUID, nejvic se pouziva ObjectId - 12 byte BSON type

schema neni explicitni, ale je spise implicitni
existuji sluzby, ktere dokazou vzit databazi a zjistit schema

Schema se muze delat bud:
- Denormalizovane - vsechna data v kazdem dokumentu
	- Lepsi pro one-to-one, one-to-many relace
	- Jednodussi dotazovani, 
- Normalizovane - data v ruznych kolekcich
	- Lepsi pro many-to-many
	- Slozitejsi dotazovani, lepsi konzistence, jednodussi update

dotazovani pomoci JSON-like constructu

