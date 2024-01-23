Technical debt describes the compromises made in software development by selecting quick-and-dirty solutions over the ideal or best ones. Such decisions might speed up the short-term development but could entail more effort in the long run due to maintenance or refactoring.

# Example
Opting for hard-coded values instead of creating a flexible configuration system because of time constraints.

# Description
Technical debt isn't always negative. Sometimes, it's a deliberate trade-off made to meet deadlines or other constraints, with the understanding that it will need addressing later.

It can either be:
- Intentional - choosing to ignore best practices knowing we need to refactor later
- Unintentional - lack of understanding, learning

# Quadrants of Tech Debt
![[tech_debt01.png]]

1. Reckless + Deliberate - no time
2. Prudent + Deliberate -  no time now, going to do it later
3. Reckless + Accidental - no knowledge
4. Prudent + Accidental - find better solution after implementation

[[Design Principles]]