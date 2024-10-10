# Dverni stanice
Building number default ID je 1
Room number (id stanice):
- Hlavni je 0
- Dalsi je 1

# Hik-connect team
Default je osboni rezim

Nove se muze vytvorit tymovy rezim

- Hik-Connect
	- Pro jednotlive uzivatele
- Team
	- Pro firmy
	- Generuje analyzy
	- Pristupy
	- Dochazka
	- Pres webovy prohlizec moznost pristupu ke kameram
	- Jednoducha vzdalena sprava
- Hik-Partner Pro
	- Vzdalena sprava pro techniky


# Nastaveni
## Dverni jednotka
1. Aktivace zarizena
	1. Nastaveni hlavniho hesla
2. Zmena IP adresy
3. Pridat
	1. Zaskrknout importovat do skupiny
	2. Pokud nyni nefunguje (Offline) => bud spatne heslo, nebo zarizeni nema internet
4. Kontrola noveho firmwaru
	1. Aktualizovat
	2. Znovu uvest do tovarniho nastaveni
	3. A znovu aktivovat (krok 1)
5. Nastaveni ve webovem rozhrani
	1. Cas
	2. Prepnout na Full HD rozhliseni
	3. Schedule
		1. Bud jde volat na jednotku
		2. nebo to ivms
	4. Intercom
		1. Floor num a ostatni = 1
		2. Door station number = cislo dverni jednotky
			1. 0 hlavni
			2. 1 a dal - vedlejsi jednotka
				1. V tom pripade je potreba nastavit IP adresu hlavni jednotky
		3. Nastaveni kodu na rele
		4. Povolit I/O
## Monitor
- je potreba prepnout tlacitko
- U kamery pro monitor je potreba nastavit u vedlejsiho streamu nastavit H264
- Dale je v kamere potreba zrusit sifrovani snimku pro Hikconnect
- Nastavit IP adresu hlavni dvorni jednotky

## Pridani cipu
1. Person IVMS
	1. Zmena jmena
	2. Lze pridavat kartu/cip:
		1. local - usb reader
		2. card reader - z dverni jednotky
2. Access control
	1. Udelit opravneni danym osobam


Je mozne pouzit software Batch Configuration
- Moznost udelat batch operace na nekolik zarizenich
	- Aktualizace
	- Reset do tovarniho nastaveni
	- A dalsi operace
- Je take mozne udelat konfiguraci pomoci Excelu