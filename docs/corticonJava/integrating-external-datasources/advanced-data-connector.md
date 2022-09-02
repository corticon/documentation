---
description: >-
  Allows decision services to read/write data using SQL queries, providing
  tremendous performance benefits when accessing certain types of data or for
  certain types of decision service architectures.
---

# Advanced Data Connectivity

#### The Basic Steps:

1. Define a mapping of your vocabulary to a database​ (same as for EDC)&#x20;
2. Craft optimized SQL queries&#x20;
3. Control when those queries are performed to retrieve data ​

[ADC ](https://documentation.progress.com/output/ua/Corticon/#page/corticon%2Foverview-of-the-advanced-data-connector.html%23)provides features that improve on EDC. With ADC, you define a mapping of your vocabulary to a database, define queries, and control when queries are performed to retrieve data from any number of sources.&#x20;

ADC functions as a service callout that accesses data as a step in a rule execution, with read/write functions through SQL queries stored in the database. You have full control over these queries. They can be parameterized so that substitutions can be performed at runtime. To make these statements easy to manage, they are also stored in a database--the same database or a database separate from the data to be queried.&#x20;

Without the constraints of Hibernate, ADC in a Decision Service has minimal processing overhead. ADC can read related data in a few passes from the database, where EDC requires discrete queries to fetch data. And ADC can write back data in chunks, where EDC writes data as discrete updates.

{% hint style="info" %}
Consider a database with these tables and relations:&#x20;

1. `Person` Table has 1,000 rows&#x20;
2. `Job` Table has 10,000 rows (10 associated Job records for each Person record)
3. `Duty`Table has 100,000 rows (10 associated Duty records for each Job)&#x20;

EDC: Could result in over 100,000 SQL queries, due to it’s ‘lazy loading’ approach.&#x20;

ADC: Only three SQL queries, one for each table, are needed to retrieve this data.
{% endhint %}

### Watch: Access Data with ADC

{% embed url="https://www.youtube.com/watch?v=kS5s20qYcec" %}

