mame system s shardingem, replikaci

Neni mozne aby takovy system byl zaroven:
1. Consistent
2. Availability
3. Partition tolerance

Musime si vybrat 2 z 3 a ten 3. trosku osidit

### Consistency
Read and write operations must be executed atomically

Musi existovat serazeni operaci, tak aby vypadaly jako kdyby byly udelane nad jednou instanci
Po zapisu musi vsichni ctenari videt stejne data

### Availability
Pokud uzel zije a prijme dotaz tak musi odpovedet

### Partition tolerance
System pokracuje fungovat i kdyz se mi sit rozbije na 2 nebo vice component 
Ne vsechny nody systemu mezi sebou muzou komunikovat, ale i tak system porad funguje

System tedy muze byt CA, CP, AP