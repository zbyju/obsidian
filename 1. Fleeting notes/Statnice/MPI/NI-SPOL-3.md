**Funkce více proměnných: gradient, Hessián, definitnost matic, extrémy funkcí více proměnných bez omezení a s rovnostními omezeními.**

# Vicerozmerny prostor a funkce
## Norma
zobrazeni $||\cdot||: V \rightarrow R_0^+$, proto ktere plati:
1. $||x|| = 0 \iff x = 0$ - jen nulovy vektor ma normu 0
2. $||\alpha x|| = |\alpha| \cdot ||x||$
3. $||x + y|| \le ||x|| + ||y||$
### Vzdalenost vektoru
d(x, y) = $||x - y||$

Plati metricke vlastnosti:
1. d(x, y) = 0 iff x = y
2. d(x, y) = d(y, x)
3. d(x, z) <= d(x, y) + d(y, z)
### Priklady norem
p-norma:
![[Pasted image 20240608161059.png]]

pro p=2 = euklidovska

maximova norma:
max(pres vsechny absolutni hodnoty vektoru)
### Okoli bodu
Mame:
- vektor (bod) $x \in R^n$
- $\delta$ realne cislo

$H_\delta(x) = \{y \in R^n | d(x, y) < \delta \}$

obecne H(x) znamena ze existuje nejake okoli bez specifikovaneho delta
### Hromadny bod
Mame:
- Mnozina $M \subset R^n$

x je hromadnym bodem M, pokud pro vsechna r > 0 plati $H_r(x) \setminus \{x\} \cap M \ne \emptyset$

x ktere neni hromadnym bodem se nazyva izolovanym bodem

= pro jakekoliv okoli bodu x najdu nejake body z M (ignoruje bod x samotny)

pro M konecna neni zadny bod hromadny
## Limita posloupnosti
Mejme posloupnost z $R^n$ (= $(x_i)^{+\infty}_{i=0}$); kde xi jsou z R^n

Posloupnost ma limitu $L \in R^n$, pokud:
### $\exists \epsilon\ \exists N_0\ \forall n > N_0: x_n \in H_\epsilon(L)$
## Funkce vice promennych
$f: D_f \rightarrow R$
$D_f \subseteq R^n$
### Graf funkce
$\Gamma\{(b_1, b_2, ..., b_n, f(b_1, b_2, ..., b_n): (b_1, b_2, ..., b_n) \in D_f\}$
### Limita funkce vice promennych
Funkce f ma limitu v bode L (z R) v hromadnem bode b mnoziny Df:
#### $\forall H(L)\ \exists H(b)\ x \in (D_f \cap H(b)) \setminus \{b\} \implies f(x) \in H(L)$
### Spojita funkce
Funkce f je spojita v bode x0 z Df pokud:
#### $\forall \epsilon > 0\ \exists \delta > 0:\ x \in (D_f \cap H_\delta(x_0)) \implies f(x) \in H_\epsilon(f(x_0))$

Funkce je spojita pokud je spojita ve vsech bodech z Df

Pomoci limity:
$lim_{x \rightarrow x_0} f(x) = f(x_0)$
### Lokalni extremy
![[Pasted image 20240608170618.png]]

# Parcialni derivace
funkce f podle smeru xi v bode b (b1, b2, ..., bn) z Df,$\exists H(b) \subset D_f$:

## $lim_{h \rightarrow 0} \frac{f(b_1, b_2, ..., b_i + h, ..., b_n) - f(b_1, b_2, ..., b_i, ..., b_n)}{h} = L$

Znacime:\
### $\partial$  

