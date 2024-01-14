# Value Type Constraint
Values of a property have a specific data type.
```turtle
ex:AgeShape a sh:PropertyShape;
  sh:path ex:age;
  sh:datatype xsd:integer. # Age must be an integer
```

# Cardinality Constraint
Specify min/max number of values of a property.
```turtle
ex:PhoneShape a sh:PropertyShape;
  sh:path ex:phoneNumber;
  sh:minCount 1; # At least one phone number required
  sh:maxCount 2. # No more than two phone numbers
```
# Value Range Constraint
Values of a property to be in a range.
```turtle
ex:AgeRangeShape a sh:PropertyShape;
  sh:path ex:age;
  sh:minInclusive 18;
  sh:maxInclusive 65. # Age must be between 18 and 65
```
# String Based Constraint
Apply constraints on string properties
```turtle
ex:EmailPatternShape a sh:PropertyShape;
  sh:path ex:email;
  sh:pattern "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$". # Regex for email
```
# Property Pair Constraint
Constraints on relationships between multiple properties.
```turtle
ex:BirthDeathDateShape a sh:NodeShape;
  sh:property [
    sh:path ex:birthDate;
    sh:lessThan ex:deathDate; # Birth date must be before death date
  ] .
```
# Logical Constraint
Impose logical constraints on properties.
```turtle
ex:LogicalShape a sh:NodeShape;
  sh:and (ex:PersonShape ex:EmployeeShape). # Must conform to both PersonShape and EmployeeShape
```
# Shape-Based Constraint
Validating other nodes connected to the focus node based on a constraint.
```turtle
ex:ProjectShape a sh:NodeShape;
  sh:targetClass ex:Project;
  sh:property [
    sh:path ex:manager;
    sh:node ex:PersonShape; # The value of 'manager' must conform to PersonShape
  ].

ex:PersonShape a sh:NodeShape;
  sh:property [
    sh:path ex:name;
    sh:datatype xsd:string;
  ];
  sh:property [
    sh:path ex:email;
    sh:pattern "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$";
  ].
```




[[_SWE Reference]]
[[2. Reference notes/SWE - Semantic Web/RDF|RDF]]
[[SHACL]]