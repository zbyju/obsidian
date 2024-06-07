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

