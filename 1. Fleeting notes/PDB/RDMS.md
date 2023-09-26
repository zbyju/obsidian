- Heap table = hromada dat, nejak je tam ten engine ulozi, negarantuje razeni

- Heap table with index = podobny pristup ale s indexem podle ktereho se k datum pristupuje
- Heap table with index se implementuje podle B* = B strom = B tree = Balanced tree nebo Bit mapy
- Neni chytry delat index nad vsim, protoze to zrychluje SELECT ale zpomaluje INSERT, UPDATE, DELETE

- Index organized table - tabulka misto pointeru jsou tam data samotne

- Cluster - data davam do bucketu
- Napr. zamestnance podle oddeleni - pak mam zamestnance v bucketech podle jejich oddleneni

- Kazdy zaznam ma sve rowid - ten popisuje primo fyzickou cestu k radku
- Podle toho se da dokonce udelat SELECT, ale ten rowid se muze zmenit = nepouzivat
- Pouziva se pro implementaci indexu