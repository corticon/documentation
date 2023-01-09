# Advanced Data Connectivity

In contrast to EDC, ADC gives IT developers much more control over which data fetch/write queries are used during rules processing. Also, contrary to EDC, multiple data sources can be combined in one single decision service. These queries are externalized in a (query) database and used when ADC is required to fetch or write data. ADC addresses a different use case compared to EDC: ADC is optimized to handle large volumes of data (potentially millions of rows) and efficiently fetches and writes data back in batched updates. In comparison with EDC, it is much (much!) quicker. So, if we need to handle a lot of data, ADC is the way to go!


[ADC ](https://documentation.progress.com/output/ua/Corticon/#page/corticon%2Foverview-of-the-advanced-data-connector.html%23)provides features that improve on EDC.

ADC uses externalized queries (stored in a query database) to fetch and write data from/to a database. 

It’s more work than EDC but gives you much more control over your queries!


ADC functions as a service callout that accesses data as a step in a rule execution, with read/write functions through SQL queries stored in the database. You have full control over these queries. They can be parameterized so that substitutions can be performed at runtime. To make these statements easy to manage, they are also stored in a database--the same database or a database separate from the data to be queried.

Without the constraints of Hibernate, ADC in a Decision Service has minimal processing overhead. ADC can read related data in a few passes from the database, where EDC requires discrete queries to fetch data. And ADC can write back data in chunks, where EDC writes data as discrete updates.

---

## Understanding ADC

Using ADC, you get great performance when processing a large dataset through a single Decision Service request. You then have access to all the data to do operations such as aggregations and clustering. You can build rules that operate on the full collection of data. 

ADC functions as a service callout that accesses data as a step in a Ruleflow. They are based on Corticon Extensions that are packaged for ADC as datasource read/write functions through SQL queries stored in the database.

To use ADC, you’ll need to:
1. Map your vocabulary to a database - In the Corticon vocabulary editor, map the entities, attributes, and associations that tell ADC how to construct entities and associations for data retrieved from the database and how to save data when storing to the database.
2. Define parameterized SQL statements for the queries - You have full control over these queries. They can be parameterized so that substitutions can be performed at runtime. To make these statements easy to manage, they are also stored in a database--the same database or a database separate from the data to be queried.
3. Add the ADC callout to a Ruleflow - In the Corticon Ruleflow editor, when you add a Service Call-out to a Ruleflow, you configure it to identify the queries to be performed by selecting one of the SQL statements you have defined. To make this easier, you can give the SQL statements logical names.

When all steps are completed, you are ready to deploy your Ruleflow or test it in the Corticon tester. When ADC runs, it performs substitutions into the statement to access data. For queries, ADC constructs entities, sets attributes, and defines associations using the Vocabulary mapping. For inserts, ADC uses the mapping data for storing to the database.

You can use multiple instances of ADC in a Ruleflow. A typical use case would be to have an instance at the start of a Ruleflow to retrieve data and one later in the Ruleflow to save data.

## Preparing a vocabulary for database integration with ADC

To use ADC, we will need to mirror our database content in our vocabulary including the table primary keys and foreign keys. For rule modelling purposes these keys are usually not used, so with EDC we generally don’t expose the primary keys in the vocabulary and foreign keys are reflected by the associations in the vocabulary. ADC is very different: we need those keys in order top read and persist our data!

!> Warning: be very meticulous naming your attributes respecting lower/upper case!!