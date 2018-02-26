# Influx DB 

```
InfluxDB is a custom high-performance data store written specifically for time series data. 
It allows for high throughput ingest, compression and real-time querying of that same data.

```
## Influx SQL 

|Action|CLI Command|
|------|-----------|
|Launch Influx CLI| influx|
|Create Database| CREATE DATABASE  databasename|
|Create User| CREATE USER username WITH PASSWORD 'userpassword' WITH privileges|
|Drop Series| drop series from measurementname|

Influx line protocol input : `measurement`,`field name=field value`,`field name 1=field value 1`_SPACE_`tag name=tag value`,`tag name1 =tag value1`_SPACE_`timestamp`


Link to Documentation [InfluxSQL](https://docs.influxdata.com/influxdb/v1.3/query_language/database_management/)

