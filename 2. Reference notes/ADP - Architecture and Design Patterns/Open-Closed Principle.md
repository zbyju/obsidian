**Definition**: Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.

**Example**: Designing a "PaymentGateway" class that can be extended to support different payment methods without altering the existing class code. New payment methods can be added as derived classes.

**Description**: OCP ensures that existing functionality remains unaltered when introducing new features, thereby safeguarding against introducing new bugs in existing features.

**Linkage:**
- [[_ADP Reference]]
- [[SOLID]]