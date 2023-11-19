# What is Timescale?

Timescale is a database platform engineered to deliver speed and scale to resource-intensive workloads, which makes it great for things like time series, event, and analytics data. Timescale is built on PostgreSQL, so you have access to the entire PostgreSQL ecosystem, with a user-friendly interface that simplifies database deployment and management.

## Hypertables
Hypertables are PostgreSQL tables that automatically partition your data by time. Interaction with hypertables is the same, but there extra features for working with time-series data easier.
Hypertables exist alongside regular PostgreSQL tables. Use hypertables to store time-series data - they give better insert, query speeds and time-series features.  Use regular PostgreSQL tables for other relational data.
Timescale improves insert and query performance by partitioning time-series data on its time parameter. Behind the scenes, the database performs the work of setting up and maintaining the hypertable's partitions. Meanwhile, you insert and query your data as if it all lives in a single, regular PostgreSQL table.