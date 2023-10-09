Vicemene nema jasnou definici
No to SQL (spis ne)
pozdeji not only SQL

Jsou to teda:
- non-relational
- casto distributed
- open-source
- horizontally scalable

Dalsi charakteristiky:
- schema-free
- easy replication
- simple API
- eventually consistent
- huge data amount

Zadny system nema tyhle featury vsechny, kazda db si zvoli svuj smer, kterym se vyda

Zakladni typy:
- key-value
- wide column
- document
- graph

dalsi typy:
- object, XML, RDF

### Key-value
dobre na cache
session data, user profile, user preference, ...
dobre kdyz se pristpuje pouze pres klic
spatne kdyz chceme limovat data


### Document stores
Document = document aggregate = jednotka dat
self describing
casto hiearchicka struktura - JSON, XML
maji nejaky ID u sebe
organizovane do kolekci

dobre na event logovani, CMS, blogy, e-commerce
dobre tam kde je hodne documentu s podobnym schema
spatny na agregovane dotazovani na hodne dokumenty
spatny kdyz se az moc meni 


### Wide column stores
column family = table = sklada se z radku
row = radek = kolekce sloupcu
sloupce pro radky se ale muzou lisit, ne vsechny radky maji stejne sloupce
hodnoty nemusi byt jen scalary ale i dalsi typy
pristupujeme typicky pres klic, umi to nejaky WHERE
nekdy se rika ze jsou podobne SQL, ale neni mozne tak dobre se dotazovat (zadny join)
vyhodne pro logovani, CMS, blogy
nepouzivat pokud chcem ACID, nebo complex dotazy

### Grafove db
Property graf = jednotka
Directed a undirected grafy
mame nody a relationships
nody i relace mohou byt asociovany s vlastnostmi
grafove databaze jsou velmi univerzalni
dobre pokud vyuzijeme grafove algo - nejkratsi cesta, kostra, sub-graf, nad-graf, queries
dobre na socialni site, routovani, dispatch, recommendation engines
nepouzivat pro extensive batch operations - davkove operace na zpracovani cele databaze, databaze je spis lepsi pro zamereni na jeden nebo dva nody a hledani vlastnosti mezi nimi

### XML Db
jsou to vicemene documentove
jsou jazyky/nastroje pro query:
XPath, XQuery, XSLT
