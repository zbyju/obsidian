**Definition**: Clients should not be forced to depend on interfaces they do not use.

**Example**: If a "Printer" interface has methods for "Print", "Scan", and "Fax", but a certain "BasicPrinter" model only supports printing, then it shouldn't have to implement "Scan" and "Fax". Instead, the interface should be broken into smaller, more specific ones.

**Description**: ISP keeps systems decoupled and easy to refactor, ensuring that implementing classes only require the methods they use, promoting clarity and reducing potential errors.