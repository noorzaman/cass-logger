# cass-logger

# Why Cassandra
Cassandra is a natural fit for ingesting large amount of logging data and store it for further troubleshooting and analytics purposes. The logs will be written constantly but analysis will be performed sporadically (relatively speaking). We will use Cassandra for storing the data for troubleshooting and analytics purposes. Cassandra provides fast insertion rates and eventual consistency. Eventual consistency means that once our data has been inserted, propagation of the data to all nodes will be done in slightly less than real time. Since this use case is for logging, transactional behavior is not anticipated where each inserted row should be available instantly to all clients.


# Schema Introduction

NOSQL databases are not very good at ad-hoc queries. This means that the use cases for querying have to be decided upfront. It seems like a massive setback but looking through most of the logging use cases, we can see that most of them fall into predictable patterns. Users need to find the raw data with some keywords and users need data stored in aggregated format for some fast queries. These are defined as:

- Raw logs where we log all the data as-is
- Part of the parsed logs to store important bits and pieces of information
- Simple rolled up data for counting different items
- Rolled up data for more involved statistics such as min, max ...
- Top N Counts for quick lookup of the best or worst performers
