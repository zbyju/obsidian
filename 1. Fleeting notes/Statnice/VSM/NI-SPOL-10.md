Systémy hromadné obsluhy a jejich limitní vlastnosti. Souvislost s Markovskými řetězci se spojitým časem.

# Model Hromadne Obsluhy
- Pozadavky prichazi nahodne s intenzitou $\lambda$ (pozadavky za jednotku)
	- Jsou zarazovany do fronty (pokud je server busy)
	- Ai = nahodny cas i-teho zakaznika od (i-1)-teho
		- $A_i$ ~ $F_A$
		- $EA_i = 1/ \lambda$
- Server vyrizuje pozadavky nahodne s intenzitou $\mu$ (pozadavky za jednotku)
	- Sj = nahodny cas obsluhy j-teho zakaznika
		- $S_i$ ~ $F_S$
		- $EA_i = 1/ \mu$
- Veliciny A1, A2, ..., S1, S2, ... jsou nezavisle
- Server obsluhuje c nezavislych obsluznych mist
	- Do fronty se zarazuje pozadavek, pokud je vsech c mist obsazenych

- Prichody se ridi Poissonovym procesem ~ $Exp(\lambda)$
- Vyrizeni pozadavku se ridi poissonovym procesem ~ $Exp(\mu)$
- Proces { X_t | t >= 0 } zaznamenava pocet pozadavku v systemu v case t
	- = proces hromadne obsluhy
- X_t je markovysky proces
- $c\mu$ - intenzita obsluhy
- $\lambda$ - intenzita prichodu
- $\rho$ = $\frac{\lambda}{c\mu}$ - pribytek pozadavku v system
	- >1 => system poroste nade vsechny meze
	- <1 => ustali se na stabilnim rozdeleni
## Kednallova notace
A|S|c
A - rozdeleni casu prichodu $F_A$
S - rozdeleni casu obsluhy $F_S$
c - pocet obsluznych mist

A a S:
- M - exponencialni rozdeleni (markovske)
- D - degenerovane rozdeleni (konstantni cas)
- G - obecne rozdeleni (nezname)
### System M|M|1
![[Pasted image 20240607191227.png]]

Neni zaruceno ze existuje stacionarni rozdeleni

Stacionarni rozdeleni existuje pokud lambda < mu:
$\pi_n = (1 - \frac{\lambda}{\mu})(\frac{\lambda}{\mu})^n$
Pro lambda > mu:
neexistuje stacionarni rozdeleni
#### Vlastnosti
$EN := E_\pi X_t$ - stredni pocet zakazniku v systemu
$EN = \sum_{n=0}^\infty n \cdot \pi_n$

Nahodna velicina W je cas straveny zakaznikem ve fronte (ne v systemu):
$P(W=0) = P(X_t = 0) = \pi_0 = 1-\rho = 1 - \frac{\lambda}{\mu}$

Pokud je v dobre prichodu v systemu n >= 1 zakazniku:
pak ma (W| Xt = n) ~ Ga(mu, n) rozdeleni

Rozdeleni doby cekani za podminky, ze zakaznik ceka:
(W|W > 0) ~ Exp(mu - lambda)
### System M|M|$\infty$
![[Pasted image 20240607193636.png]]
## Exponencialni zavody
Ve fronte je n-1 pozadavku (v system n pozadavku) = Xt = n

Serveru bezi exponencialni hodiny S ~ Exp(mu)
Front bezi exponencialni hodiny T ~ Exp(lambda)

Probihaji exponencialni zavody mezi nahodnymi casy S a T
Zavody skonci v case $\tau = min\{S, T\}$

Pokud vyhraje server pak: $X_{t+\tau}=n-1$
Pokud vyhraje fronta pak: $X_{t+\tau}=n+1$

### Vlastnosti Exp zavodu
![[Pasted image 20240607162725.png]]
### Vitez exp zavodu
$P(T < S) = \frac{\lambda}{\lambda + \mu}$
$P(S < T) = \frac{\mu}{\lambda + \mu}$
# Littleho veta
