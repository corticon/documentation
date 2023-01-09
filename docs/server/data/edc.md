## Simple Database Connectivity

EDC allows you read data from a single relational database and persist the rule evaluation data) back into that same database. In general, rule authors find it easy to use/setup (high productivity) as no coding is required to fetch and write data. EDC has been purposely designed for a very common use case scenario which is single transaction enrichment (e.g. you pass Corticon an Order ID and EDC will look up all additional order details including data from related tables. Data is pulled in selectively in case it is needed in the rules (lazy loading). 

As EDC is using the Java data Hibernate framework, there is a drawback in terms of performance. EDC is not designed to handle large volumes typically found in transaction rich batch processes due to the (relative inefficient) way it queries and updates databases.


## Pros and Cons

|                            Benefits                            |                              Drawbacks                              |
| :-------------------------------------------------------------: | :------------------------------------------------------------------: |
|            Model driven approach – No SQL/JDBC code            |                           Limited to RDBMS                           |
|    Database independence – Rules don’t change if data does    |                Require good DB schema (PKs, FKs, etc)                |
| Minimize client application re-factoring when data needs change |                Require JDBC connectivity to database                |
|    Leverages industry leading Progress DataDirect technology    | Poor performance for large datasets due to ‘chatty’ DB interaction |

