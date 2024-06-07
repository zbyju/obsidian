**Markovské řetězce se spojitým časem. Souvislost s Markovskými řetezci s diskrétním časem a s Poissonovým procesem.**

# Poissonuv proces
## Citaci proces
Nahodny proces {Nt|t >= 0} je citaci proces pokud:
1. Nt >= 0 - trajektorie jsou nezaporne
2. Nt ze Z - trajektorie jsou celociselne
3. s <= t => Ns <= Nt - neklesajici
### Binomicky proces
Citaci proces je binomicky, pokud casy mezi udalostmi jsou nezavisle a geometricky rozdelene

binomicky proces -> spojity ekvivalent = misto geometrickeho rozdeleni exponencialni (obe jsou bezpametove)

## Poissonuv proces
{ Xj | j z N } iid nahodne veliciny s rozdelenim Exp($\lambda$)

Definujeme { Tn | n z N }: 
### $T_0 = 0$
### $T_n = T_{n-1} + X_n = \sum_{j=1}^n X_j; n \ge 1$

Cas prvni udalosti je 0; cas n-te udalosti je v case n-1 udalosti + n ty cas z exponencialniho rozdeleni = cas n-te udalosti je cas vyscitany od 1. udalosti do n

Pak nahodny proces $\{N_t | t \in [0, \infty)\}$, kde:
### $N_t = max\{n \in N_0 | T_n(\omega) \le t \}$
Nazveme poissonuv proces

Poissonuv proces mi rekne pro kazde t, kolik nastalo udalosti do casu t. Modeluje nezavisle udalosti mezi kterymi neni zadna interakce. 
### Alternativne
![[Pasted image 20240606231447.png]]
#### Exponencialni rozdeleni
![[Pasted image 20240606232419.png]]
##### Bezpametovost
T ~ Exp(lambda) exponencialni rozdeleni, pak pro vsechna t, s >= 0:
P(T > t + s | T > t) = P(T > s)
= pokud jsem cekal t minut, pak pravdepodobnost, ze budeme cekat dalsich s minut je stejna jako kdybychom necekali.

= bezpametovost
##### Soucet exponencialnich je gamma

### Vlastnosti
![[Pasted image 20240606231630.png]]

### Ekvivalentni definice Poissonova procesu
![[Pasted image 20240606232947.png]]

## Markovsky retezec se spojitym casem
Nahodny proces $\{X_t | t \ge 0 \}$ s nejvyse spocetnou mnozinou stavu S je markovsky retezec se spojitym casem, pokud splnuje Markovskou podminku:
![[Pasted image 20240606233331.png]]

Rozdeleni v case t pro stav i:
$p_i(t) := P(X_t = i)$

Matice pravdepodobnosti prechodu:
$P_{ij}(t, s) = P(X_s = j | X_t = i)$
#### Vlastnosti
![[Pasted image 20240606233506.png]]
#### Homogenni markovsky retezec
![[Pasted image 20240606233615.png]]
#### Matice skokovych intenzit
![[Pasted image 20240606233733.png]]

Tato matice ma jako sve prvky vlastne derivace funkci P v nule.

Na diagonale odecitam 1, jinak ne. => na diagonale mam hodnoty <= 0
Mimo diagonalu mam hodnoty >= 0
celkove se mi radek vyscita na 0 => Qii = suma vsech ostatnich prvku v danem radku
##### Simulace procesu pomoci skokovych intenzit
![[Pasted image 20240606235331.png]]
1. cas do vyskoku je skokova ma exp rozdeleni s intenzitou na diagonale
2. pravdepodobnost ze retezec skoci z i do j je rozdelen pomerne mezi vsechny mozne j

-Qii = suma Qik