# DynamoDB

## RDS OLTP Relational DBs
* MS SQL Server
* Oracle
* MySQL
* PostgresSQL
* Aurora
* MariadB

## Non-relational DB
* DynamoDB - no SQL
* Redshift - OLAP datawarehousing
* Elasticache - in memory caching.
* DMS

## How to improve db speed?
* Elasticache - either Memcached or Redis.
* It will cache the most consistently queried aspects of your DB.

## DMS - database migration service
* Allows you to migrate your DB to AWS automatically.

## DyanmoDB Facts
* document oriented - collection (table), document(row), key/value pair (fields).
* Single-ditig millisecond latency
* On SSD
* Spread across 3 geographically distinct data centers

## Consistency modes
* Eventual consistent reads (default). Consistency is delayed, but is reached within 1 seconds.
* Strongly consistent reads - consistent immediately prior to the read.

## Basics
* Table - e.g. school
* Items - row of data. e.g. students.
* Attribute - e.g. a student's first name.
* 35 levels of nesting within a json item (row).
* You can export table or items into CSV.

## Lab
* Give EC2 IAM role of AmazonDynamoDBFullAccess.

## Primary Keys (unique IDs)
* Two types of primary keys:
1. **Single Attribute** primary key (i.e. unique id). aka **Partition Key** aka **Hash Key**. 
    DyanmoDB uses this as input to an internal hash function. 
    The output from the hash function determines the partition (the physical location in which data is stored).
2. **Composite** primary key (eg. unique id + data range) aka **Partion key + Sort Key** aka Hash + range. 
    e.g. same person (same unique key) posting on a forum at different times (i.e. thread in reddit). Time stamp have to be different.

## Indexes
* Local Secondary Index - same Partition key, different sort key. Must be created when table is first created. Can't be modified or deleted. 
* Global Secondary Index - different partition key, different sort key. Can be created at table creation or added later.
* Max 5 local secondary index.
* Max 5 secondary index.

## Streams
* captures any modifications to the tables.
* if a new item is added to the table, the stream captures an image of the entire item + all its attributes. Stores it for 24hrs.
* if item is updated, stream captures "before" and "after" images of modified attributes.
* if item is deleted, stream captures image of entire item before it was deleted. 

## Triggers
* Connect Streams to lambda.
* modify item, stream is triggers, lambda is triggered.

