0. Many times we start with [[Factory Method Pattern]] and then switch to [[Abstract Factory Pattern]] when it's not enough
1. Map out various distinct product types vs variants of these products
	- Product types: Chair, Table
	- Variants: Spherical, Pyramidal
	- Not all product types might support all variants (e.g. there is no pyramidal chair)
2. Make abstract products for all product types and inherit from them for con