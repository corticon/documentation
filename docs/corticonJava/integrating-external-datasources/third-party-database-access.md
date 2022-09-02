---
description: >-
  If you need custom database access beyond that provided by Corticon's
  Enterprise Data Connector (EDC) or Advanced Data Connector (ADC) you can now
  use the DataDirect® drivers bundled with Corticon.
---

# Third Party Database Access

Corticon provides a new factory method for getting a connection to a database. It connects to a database using a DataDirect driver and returns a standard `java.sql.Connection` object. You work with this Connection object the same as you would any Connection in Java.

The `ICcDataObjectManager` class now provides a method to retrieve an instance of `IDatabaseDriverManager`. This new class provides the `getConnection(…)` method that can be used to create a database connection using a bundled DataDirect driver. See the Corticon JavaDoc for details on these classes and methods.

### Get a connection <a href="#d1500e75" id="d1500e75"></a>

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

### Close a connection <a href="#d1500e215" id="d1500e215"></a>

When you have completed processing requests, you can either:

* Close the connection using the `close()` method in the `Connection` interface. In some cases, you want to immediately release a connection's database and JDBC resources instead of waiting for them to be automatically released; the `close()` method provides this immediate release.
* Leave the connection up when connection pooling is being used.
* Leave the connection open until the JVM exits or the class gets garbage collected.
