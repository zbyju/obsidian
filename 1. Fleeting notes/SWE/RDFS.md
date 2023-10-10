RDF Schema
Semantics for classes and properties

RDF popisuje resources
RDFS definuje jazyk pro vytvareni terminologie (slovniku)
Je mozne pak vytvaret zakladni ontologii a hiearchii
Staci specifikovat tu nejvic specifickou informaci o resource a zbytek uz se inferne ze zbytku hiearchie (Alice is a Woman, no need to specify Alice is a Person, to uz bude inferred z toho ze Woman je subclass Person).

relace:
- rdfs:subclassOf
- rdfs:subpropertyOf
- rdfs:range - pro property specifikuje co za typ musi byt na strane object
- rdfs:domain - pro property 

Subject - Property - Object
^ domain -             - range ^