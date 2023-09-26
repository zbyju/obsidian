1. Data mam na disku
3. Databaze ma Database buffer cache
4. Data nacitame z disku do RAM
5. Dat je obecne vic nez RAM
6. Heruistiky se snazi zlepsit pristup k datum, aby jich bylo co nejvice v RAM

Pri presunu dat z disku do RAM se to deje po blocich = database data block, asi 8kB

Pokud chceme pristoupit k jednomu radku (treba 50B) je potreba nacist cely datovy blok (8kB)