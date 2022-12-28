# Accessing Data from Decision Services

In most Corticon deployments, the data is passed in. This simplifies the architecture because you don't need to account for Corticon connecting to external data sources. This is especially true when you have legacy systems which cannot be easily accessed.

In some cases, the data passed in can be large. For example, all the data needed to process a loan application for a single applicant. In some deployments, Corticon needs to retrieve supporting data. This adds another connection to the architecture, yet it can be a considerable savings to not have to pass in all the data in the request. This is especially true where the data is selective – when the rules are choosing some subset of data that is needed. This can also be useful with reference data that you want to cache.

In other deployments Corticon needs to retrieve the data for efficiency. An example would be a batch application where you need to process a billion records at the end of the month. In such cases, efficient moving of data is essential for performance.

## Data Integration Tutorials

* [Modeling Progress Corticon Rules to Access a Database using EDC](https://docs.progress.com/bundle/corticon-edc-modeling-tutorial/page/Tutorial-Modeling-Progress-Corticon-Rules-to-Access-a-Database-using-EDC.html)
* [Connecting a Progress Corticon Decision Service to a Database using EDC](https://docs.progress.com/bundle/corticon-connect-to-db-using-edc/page/Tutorial-Connecting-a-Progress-Corticon-Decision-Service-to-a-Database-using-EDC.html)
