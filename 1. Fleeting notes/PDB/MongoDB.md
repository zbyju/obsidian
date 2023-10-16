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
	- Jednodussi dotazovani, muze byt problem s konzistenci, slozitejsi updaty
- Normalizovane - data v ruznych kolekcich
	- Lepsi pro many-to-many
	- Slozitejsi dotazovani, lepsi konzistence, jednodussi update
	- Reference pomoci direct linku (reference) - id jineho objektu
		 - 

Insert
- insertOne, insertMany

update
- replaceOne, updateOne, updateMany

remove
- deleteOne, deleteMany

find

dotazovani pomoci JSON-like constructu

Mongo nabizi dotazy pomoci nekolika casti - query (selekce), projekce, sort, skip, limit
navic nabizi dalsi utility pomoci $operator:
$eq, $ne, $lt, $lte, $gt, $gte, $in, $nin, $exists, $regex, ...

Value equality can be tricky
- scalars must have the same value
- objects must have the same value, including the order attributes (names)
	- { name: "x", age: 10 } is not the same as { age: 10, name: "x" } 
	- better to use dot notation object.name: "x", object.age: 10
- arrays must have the same value, including the order

Pokud potrebujeme "join" tabulek, pak je to mozne pomoci aggregate a nasledne $lookup. V nejakych driverech pak je mozne pouzit zjednodusene konstrukty (mongoose populate) to ale neni cast MongoDB

