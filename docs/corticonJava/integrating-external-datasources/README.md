# Accessing Data from Decision Services

Corticon Server Deployments provide the flexibility to either pass the data in on the call to the decision service or to have the decision service retrieve data, or a mix of both.

In most Corticon deployments, the data is passed in. This simplifies the architecture because you don't need to account for Corticon connecting to external data sources. This is especially true when you have legacy systems which cannot be easily accessed.

In some cases, the data passed in can be large. For example, all the data needed to process a loan application for a single applicant. In some deployments, Corticon needs to retrieve supporting data. This adds another connection to the architecture, yet it can be a considerable savings to not have to pass in all the data in the request. This is especially true where the data is selective – when the rules are choosing some subset of data that is needed. This can also be useful with reference data that you want to cache.

In other deployments Corticon needs to retrieve the data for efficiency. An example would be a batch application where you need to process a billion records at the end of the month. In such cases, efficient moving of data is essential for performance.

## Simple Database Connectivity

Corticon [EDC ](https://documentation.progress.com/output/ua/Corticon/#page/corticon%2Fidentity-strategies.html%23)is designed to augment data when processing a discrete Decision Service request. It is used by rule authors who seek the least-technical requirements for modeling data access in their rules, to read/write to an external relational database. However, because it is built on Hibernate and is tied to Hibernate’s object relational model and transactional models, it introduces query and data processing overhead when reading data from a database with related tables. So, EDC's limitations are in its performance in large, data intensive operations where large chunks of data are loaded into Corticon for processing and updating the connected database. Corticon ships with Progress DataDirect drivers for RDBMSs, but you can also use the drivers bundled to[ create new database connections](https://documentation.progress.com/output/ua/Corticon/#page/corticon%2Fusing-datadirect-drivers.html%23).

### Summary: Enterprise Data Connector

|                             Benefits                            |                              Drawbacks                             |
| :-------------------------------------------------------------: | :----------------------------------------------------------------: |
|             Model driven approach – No SQL/JDBC code            |                          Limited to RDBMS                          |
|     Database independence – Rules don’t change if data does     |               Require good DB schema (PKs, FKs, etc)               |
| Minimize client application re-factoring when data needs change |                Require JDBC connectivity to database               |
|    Leverages industry leading Progress DataDirect technology    | Poor performance for large datasets due to ‘chatty’ DB interaction |


## Advanced Data Connectivity

Corticon's Advanced Data Connectivity  alows decision services to read/write data using SQL queries, providing tremendous performance benefits when accessing certain types of data or for certain types of decision service architectures.

### The Basic Steps:

1. Define a mapping of your vocabulary to a database​ (same as for EDC)
2. Craft optimized SQL queries
3. Control when those queries are performed to retrieve data ​

[ADC ](https://documentation.progress.com/output/ua/Corticon/#page/corticon%2Foverview-of-the-advanced-data-connector.html%23)provides features that improve on EDC. With ADC, you define a mapping of your vocabulary to a database, define queries, and control when queries are performed to retrieve data from any number of sources.

ADC functions as a service callout that accesses data as a step in a rule execution, with read/write functions through SQL queries stored in the database. You have full control over these queries. They can be parameterized so that substitutions can be performed at runtime. To make these statements easy to manage, they are also stored in a database--the same database or a database separate from the data to be queried.

Without the constraints of Hibernate, ADC in a Decision Service has minimal processing overhead. ADC can read related data in a few passes from the database, where EDC requires discrete queries to fetch data. And ADC can write back data in chunks, where EDC writes data as discrete updates.

> Consider a database with these tables and relations:
> 1. `Person` Table has 1,000 rows
> 2. `Job` Table has 10,000 rows (10 associated Job records for each Person record)
> 3. `Duty`Table has 100,000 rows (10 associated Duty records for each Job)
> EDC: Could result in **over 100,000 SQL queries**, due to it’s ‘lazy loading’ approach.
> ADC: **Only three SQL queries,** one for each table, are needed to retrieve this data.


## REST Data Connectivity

The Corticon REST Datasource provides support for accessing REST services. It allows you to retrieve REST data to enrich the payloads being processed by your rules.

The Corticon REST Datasource uses the DataDirect [Autonomous REST Connector ](https://www.progress.com/connectors/autonomous-rest-connector)which provides the ability to access REST services as if they were databases. This is beneficial to a Corticon user because the process of mapping a vocabulary to a REST service is the same as for EDC and ADC data sources.


### Mapping vocabulary to a REST datasource

To configure the REST Datasource you either perform schema discovery or supply your own schema file. When using schema discovery, you supply the URL of the REST data source and query parameters and allow the Autonomous REST Connector to generate a schema for your REST service. To supply your own schema, you can either export a discovered schema from Corticon Studio and make edits or create one from scratch. See the[ Autonomous REST Connector documentation](https://docs.progress.com/bundle/corticon-data-integration/page/Overview-of-the-Autonomous-REST-Connector.html) for details on the its schema file format.

The query parameters for a REST Datasource can either be fixed or dynamically set by data in your payload. Dynamic setting of parameters allows you to access a REST service to retrieve information about a specific entity in your payload. You can also configure the security settings for accessing a REST service.

As REST access is limited to read-only, it is ideal for data enrichment. You could have one or several REST Datasources used by a decision service. You can even mix EDC or ADC with REST depending on your data access needs.

The wealth of REST data sources exposed through APIs means that you could be touching multiple sources to build the best complete data set possible. In marketing scenarios that might mean taking sparse info on a prospect from social or business contacts to enrich the data by discovering their profile and preferences to focus campaigns and assign local reps for follow-up. In medical applications, diagnoses and treatments can be enriched with claims approval histories or related clinical trials. For mortgage lenders, quickly scanning multiple credit review resources for a prospect, and then matching their home value and loan to retrieve the best rate from multiple lenders.

### More REST Connectivity Resources
- [Integrate REST API Data into Your Business Rules with Corticon 6](https://www.youtube.com/watch?v=kRx5JgHXGDU&list=PLC679RvCan2CoOLaYQzUEriM3WS-UFQ5N&index=3)
- [Getting Started with REST](https://docs.progress.com/bundle/corticon-data-integration/page/Getting-Started-with-REST.html) on Corticon Information Hub.


## Batch Processing

Batch execution is designed to process large volumes of records in a database. Batch jobs are scheduled in the Web Console or can be set up using cron facilities or other scheduling software. If you use an alternative to the Web Console to manage batch jobs, you can use it and call Corticon’s REST API to start a batch process.

Technically, ADC is not required, but the intent is that ADC would be used. What is required is a Query datasource for the use of the built in batch capabilities. The query datasource provides seed records to process such as customer IDs. The paradigm is that Corticon’s batch controller retrieves the seed records from the Query datasource in large chunks and then passes them in for rule processing where the rules will use ADC to retrieve additional data for those records.&#x20;

The built in batch processing is optimized for large data sets – millions or even billions of records to be processed on a set schedule. It can be used with smaller data sets but knowing that it’s designed for large data sets helps  to understand it’s optimization around the use of a Query and ADC datasources.

The built in support is not the only way to do batch processing with Corticon. We have customers with bespoke solutions doing things like having Corticon embedded in a message client or pulling payload from an S3 bucket.&#x20;

Fetching the transaction identifying data from the underlying relational data source that will be injected into the rules engine takes place outside the Decision Service. As such, Decision Service requests that are usually individual transactions are instead fetched in chunks for the rules engine, and then dispersed across multiple processing threads to concurrently process the incoming requests. Batch processing produces no return payload per request -- the result of each rule processing is persisted in the database. In this format, one of our biggest public sector clients scales their Corticon horizontally with s3, bringing up hundreds of servers for specific windows of time in bursts each month.

### To learn more, see [Getting Started with Batch](https://docs.progress.com/bundle/corticon-data-integration/page/Getting-Started-with-Batch.html) on Corticon Information Hub.


## Third Party Database Access

If you need custom database access beyond that provided by Corticon's Enterprise Data Connector (EDC) or Advanced Data Connector (ADC) you can use the DataDirect drivers bundled with Corticon.

Corticon provides a  factory method for getting a connection to a database. It connects to a database using a DataDirect driver and returns a standard `java.sql.Connection` object. You work with this Connection object the same as you would any Connection in Java.

The `ICcDataObjectManager` class now provides a method to retrieve an instance of `IDatabaseDriverManager`. This new class provides the `getConnection(…)` method that can be used to create a database connection using a bundled DataDirect driver. See the Corticon JavaDoc for details on these classes and methods.

### Get a connection 

The class `CcDatabaseConnectionFactory` opens a connection to the database and processes queries. It contains a method that returns a `java.sql.Connection` interface to open a connection using the DataDirect driver and returning it. The `getConnection()` method returns a `java.sql.Connection` from these signatures:

```
getConnection(String dataSourceId, String driverId, String connectionString, String username, String password)
```

* String: `dataSourceId` - The JNDI dataSource Id. This value is used to lookup an existing connection.
* String: `driverID` - The Id (as outlined in `DatabaseDefinitions.xml`) for the DataDirect driver.
* String: `ConnectionString` - Driver connection string, in the same format as EDC connection in Corticon Studio. For example, `jdbc:progress:openedge://hostname:5566;databaseName=corticon`
* String: `username` - username for logging into the database.
* &#x20;String: `password` - password for logging into the database.

```
getConnection(String dataSourceId, String driverId, String host, int Port, String databaseName, String username, String password)
```

* String: `dataSourceId` - The JNDI dataSource Id. This value is used to lookup an existing connection.
* String: `driverID` - The Id (as outlined in `DatabaseDefinitions.xml`) for the DataDirect driver.
* String: `host` - The hostname of the database server for connection.
* Int : `Port` - Port number of the database server for connection.
* String: `databaseName` - the name of the database for connection on the server .
* String: `username` - username for logging into the database.
* String: `password` - password for logging into the database.

```
getConnection(String dataSourceId)
```

* String: `dataSourceId` - The JNDI dataSource Id. This value is used to lookup an existing connection.

```
getConnection(Properties connectionProperties)
```

* &#x20;Properties: _`properties`_ - Object passed with each of the above items as fields. This also lets you specify additional connection parameters. Constants for the properties fields will be supplied.

### Close a connection 

When you have completed processing requests, you can either:

* Close the connection using the `close()` method in the `Connection` interface. In some cases, you want to immediately release a connection's database and JDBC resources instead of waiting for them to be automatically released; the `close()` method provides this immediate release.
* Leave the connection up when connection pooling is being used.
* Leave the connection open until the JVM exits or the class gets garbage collected.

## Data Connectivity Tutorials

* [Modeling Progress Corticon Rules to Access a Database using EDC](https://docs.progress.com/bundle/corticon-edc-modeling-tutorial/page/Tutorial-Modeling-Progress-Corticon-Rules-to-Access-a-Database-using-EDC.html)
* [Connecting a Progress Corticon Decision Service to a Database using EDC](https://docs.progress.com/bundle/corticon-connect-to-db-using-edc/page/Tutorial-Connecting-a-Progress-Corticon-Decision-Service-to-a-Database-using-EDC.html)
