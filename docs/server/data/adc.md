# Advanced Data Connectivity

In contrast to EDC,  ADC gives IT developers much more control over which data fetch/write queries are used during rules processing. Also, contrary to EDC, multiple data sources can be combined in one single decision service. These queries are externalized in a (query) database and used when ADC is required to fetch or write data. ADC addresses a different use case compared to EDC: ADC is optimized to handle large volumes of data (potentially millions of rows) and efficiently fetches and writes data back in batched updates. In comparison with EDC, it is much (much!) quicker. So, if we need to handle a lot of data, ADC is the way to go!


[ADC ](https://documentation.progress.com/output/ua/Corticon/#page/corticon%2Foverview-of-the-advanced-data-connector.html%23)provides features that improve on EDC. With ADC, you define a mapping of your vocabulary to a database, define queries, and control when queries are performed to retrieve data from any number of sources.

ADC functions as a service callout that accesses data as a step in a rule execution, with read/write functions through SQL queries stored in the database. You have full control over these queries. They can be parameterized so that substitutions can be performed at runtime. To make these statements easy to manage, they are also stored in a database--the same database or a database separate from the data to be queried.

Without the constraints of Hibernate, ADC in a Decision Service has minimal processing overhead. ADC can read related data in a few passes from the database, where EDC requires discrete queries to fetch data. And ADC can write back data in chunks, where EDC writes data as discrete updates.
