# What is Timescale?

Timescale is a database platform engineered to deliver speed and scale to resource-intensive workloads, which makes it great for things like time series, event, and analytics data. Timescale is built on PostgreSQL, so you have access to the entire PostgreSQL ecosystem, with a user-friendly interface that simplifies database deployment and management.

## Hypertables
Hypertables are PostgreSQL tables that automatically partition your data by time. Interaction with hypertables is the same, but there extra features for working with time-series data easier.
Hypertables exist alongside regular PostgreSQL tables. Use hypertables to store time-series data - they give better insert, query speeds and time-series features.  Use regular PostgreSQL tables for other relational data.
Timescale improves insert and query performance by partitioning time-series data on its time parameter. Behind the scenes, the database performs the work of setting up and maintaining the hypertable's partitions. Meanwhile, you insert and query your data as if it all lives in a single, regular PostgreSQL table.
Each hypertable is made up of child tables called chunks. Each chunk is assigned a range of time, and only contains data from that range. If the hypertable is also partitioned by space, each chunk is also assigned a subset of the space values.

### Time partitioning
Each chunk of a hypertable only holds data from a specific time range. When you insert data from a time range that doesn't yet have a chunk, Timescale automatically creates a chunk to store it.
By default, each chunk covers 7 days. You can change this to better suit your needs. For example, if you set `chunk_time_interval` to 1 day, each chunk stores data from the same day. Data from different days is stored in different chunks.
![[Pasted image 20231119212950.png]]
#### Best practices
Chunk size affects insert and query performance. You want a chunk small enough to fit into memory. This allows you to insert and query recent data without reading from disk. But you don't want too many small and sparsely filled chunks. This can affect query planning time and compression.

We recommend setting the `chunk_time_interval` so that 25% of main memory can store one chunk, including its indexes, from each active hypertable. You can estimate the required interval from your data rate. For example, if you write approximately 2 GB of data per day and have 64 GB of memory, set the interval to 1 week. If you write approximately 10 GB of data per day on the same machine, set the time interval to 1 day.

Be aware that indexes might take a lot of space if they are complex (e.g. geospatial). [`chunks_detailed_size`](https://docs.timescale.com/api/latest/hypertable/chunks_detailed_size) function can say more about the size.
#### Hypertable indexes
By default, indexes are automatically created when you create a hypertable. You can prevent index creation by setting the `create_default_indexes` option to `false`.

The default indexes are:
- On all hypertables, an index on time, descending
- On hypertables with space partitions, an index on the space parameter and time

Hypertables have some restrictions on unique constraints and indexes. If you want a unique index on a hypertable, it must include all the partitioning columns for the table. To learn more, see the section on [creating unique indexes on a hypertable](https://docs.timescale.com/use-timescale/latest/hypertables/hypertables-and-unique-indexes/).

## [Time buckets](https://docs.timescale.com/use-timescale/latest/time-buckets/#time-buckets)
Time buckets ([`time_bucket`](https://docs.timescale.com/api/latest/hyperfunctions/time_bucket/) function, similar to PostgreSQL's [`date_bin`](https://www.postgresql.org/docs/current/functions-datetime.html#FUNCTIONS-DATETIME-BIN) function, but gives more flexibility for bucket size and start time) enable you to aggregate data by time interval. For example, you can group data into 5-minute, 1-hour, and 3-day buckets to calculate summary values.

Time bucketing is essential to working with time-series data. You can use it to roll up data for analysis or downsampling. For example, you can calculate 5-minute averages for a sensor reading over the last day. You can perform these rollups as needed, or pre-calculate them in [continuous aggregates](https://docs.timescale.com/use-timescale/latest/continuous-aggregates/).

### How time bucketing works
Time bucketing groups data into time intervals. With `time_bucket`, the interval length can be any number of microseconds, milliseconds, seconds, minutes, hours, days, weeks, months, years, or centuries.

The `time_bucket` function is usually used in combination with `GROUP BY` to aggregate data. For example, you can calculate the average, maximum, minimum, or sum of values within a bucket.

![[Pasted image 20231119214923.png]]

#### Origin
The origin determines when time buckets start and end. By default, a time bucket doesn't start at the earliest timestamp in your data. There is often a more logical time. For example, you might collect your first data point at `00:37`, but you probably want your daily buckets to start at midnight. Similarly, you might collect your first data point on a Wednesday, but you might want your weekly buckets calculated from Sunday or Monday.

Instead, time is divided into buckets based on intervals from the origin. The following diagram shows how, using the example of 2-week buckets. The first possible start date for a bucket is `origin`. The next possible start date for a bucket is `origin + bucket interval`. If your first timestamp does not fall exactly on a possible start date, the immediately preceding start date is used for the beginning of the bucket.

![[Pasted image 20231119231531.png]]

In other words you set some origin datetime and then you calculate the time buckets from that point instead of using the first value.
##### [Default origins](https://docs.timescale.com/use-timescale/latest/time-buckets/about-time-buckets/#default-origins)
There are some sensible default origins (start on Monday at 00:00:00 etc), the default origin can be changed through 