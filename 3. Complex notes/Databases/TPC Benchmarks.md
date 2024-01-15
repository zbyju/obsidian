Stands for Transaction Processing Performance Council - organization that defines and maintains a set of standardized benchmarks for evaluating database performances.

They define different benchmarking scenarios to test real-world performance.

# TPC-C
It is one of the most known benchmarks by TPC. The primary focus is on OLTP systems. It simulates a scenario of a simple eshop - making an order, payment, ...

Output:
- tpmC - transactions per minute - the number of new order transactions per minute a system can process.
- $/tpmC - transactions per minute cost - best value configuration

# TPC-E
Similar to TCP-C it focuses on OLTP systems. It simulates a scenario of a trading company and is more complex than TPC-C which had way less tables and had artificial data. TCP-E has real-world data and many more tables. Also has some constraints.

Output:
- tpsE - Number of business transactions processed per second.
- $/tpsE - bank for buck

# TPC-H
Benchmark for decision support = OLAP. It simulates an environment where users run ad-hoc queries on a large dataset. They are designed to simulate real-world decision support scenarios - aggregating, joining and sorting large volumes of data. It focus on read-only queries.

Output:
- QphH - Queries per Hour


