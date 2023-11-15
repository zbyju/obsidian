- A design pattern that defers the initialization of an object until the point at which it is needed.
- Can improve the efficiency of a system, especially when dealing with heavy resources or large amounts of data.

*Example: Database: entire records might not be loaded into memory immediately. Instead, the data is fetched lazily when accessed by the application. This approach is particularly useful when working with large datasets where loading all data at once would be inefficient or impractical.*