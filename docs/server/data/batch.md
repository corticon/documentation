# Batch Processing

## Overview

Batch execution is designed to process large volumes of records in a database. Batch jobs are scheduled in the Web Console or can be set up using cron facilities or other scheduling software. If you use an alternative to the Web Console to manage batch jobs, you can use it and call Corticon’s REST API to start a batch process.

Technically, ADC is not required, but the intent is that ADC would be used. What is required is a Query datasource for the use of the built in batch capabilities. The query datasource provides seed records to process such as customer IDs. The paradigm is that Corticon’s batch controller retrieves the seed records from the Query datasource in large chunks and then passes them in for rule processing where the rules will use ADC to retrieve additional data for those records.&#x20;

The built in batch processing is optimized for large data sets – millions or even billions of records to be processed on a set schedule. It can be used with smaller data sets but knowing that it’s designed for large data sets helps  to understand it’s optimization around the use of a Query and ADC datasources.

The built in support is not the only way to do batch processing with Corticon. We have customers with bespoke solutions doing things like having Corticon embedded in a message client or pulling payload from an S3 bucket.&#x20;

Fetching the transaction identifying data from the underlying relational data source that will be injected into the rules engine takes place outside the Decision Service. As such, Decision Service requests that are usually individual transactions are instead fetched in chunks for the rules engine, and then dispersed across multiple processing threads to concurrently process the incoming requests. Batch processing produces no return payload per request -- the result of each rule processing is persisted in the database. In this format, one of our biggest public sector clients scales their Corticon horizontally with s3, bringing up hundreds of servers for specific windows of time in bursts each month.

To learn more, see [Getting Started with Batch](https://docs.progress.com/bundle/corticon-data-integration/page/Getting-Started-with-Batch.html) on Corticon Information Hub.
