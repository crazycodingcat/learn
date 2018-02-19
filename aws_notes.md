## Data Warehousing
- used for business intelligence. Tools like Congnos, Jaspersoft, SQL Server Reporting Services
- used to pull in very large and complex data sets to do queries on data.

### OLTP vs OLAP
- OLTP: e.g. order number 21201, pulls out the row for this order number
- OLAP: e.g. sum of xxx, pulls in large numbers of records

## DynamoDB
- expensive for writes, cheap for reads
- push button scaling, no downtime

## Redshift
- Columnar data storage -  good for data warehousing and analytics, where queries often involve aggregates performed over large data sets. (Row-based systems are ideal for transaction processing)
- Data stored on disk sequentially (columms)
- Advanced compression
- MPP

## Elasticache
- a web service that makes it easy to deploy, operate and scale an in-memory cache in the cloud.
- supports Memcached and Redis

## S3:
- Object based storage (flat files). Not blob based storage
- key-value store  object name - object content