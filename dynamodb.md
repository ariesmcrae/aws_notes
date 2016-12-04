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
* **Eventual consistent** reads (default). Consistency is delayed, but is reached within 1 seconds.
* **Strongly consistent** reads - consistent immediately prior to the read.

## Basics
* Table 
* Items - row. e.g. students.
* Attribute - column e.g. a student's first name.
* 35 levels of nesting within a json item (row).
* You can export table or items into CSV.

## Lab
* Give EC2 IAM role of AmazonDynamoDBFullAccess.

## Primary Keys (unique IDs)
* Two types of primary keys:
1. **Single Attribute** primary key aka **Partition Key** aka **Hash Key**. 
    DyanmoDB uses this as input to an internal hash function. 
    The output from the hash function determines the partition (the physical location in which data is stored).
2. **Composite** - **Partion key + Sort Key**. 
    e.g. same person (same primary key) posting on a forum at different times (i.e. thread in reddit). Time stamp have to be different.

## Indexes
* Local Secondary Index - same Partition key (primary key), different sort key. Must be created when table is first created. Can't be modified or deleted. 
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

## Query API Call
* Query - searches only partition key (primary key) + sort key.
* Returns data matching primary key search.
* Very efficient. Searches indexes only.
* All attribs of an item is returned. but you can use ProjectionExpression parameter so that the query only returns some of the attributes.
* Result is sorted by sort key **ascending**. To make it **descending**, set the **ScanIndexForward** param to **false**.
* by default, it is **eventually consistent**, but can be changed to **strongly consistent**.
![](./images/dynamodb_query.jpg)



## Scan 
* Returns all items (and their attribues) in the table; therefore very inneficient.
* It scans the entire table, then filters out the values to provide the desired results, essentially adding the extra step of removing data from the result set.
* You can use **ProjectionExpression** param so that scan only returns some attribues.
* Only eventual consistent reads are available (not strong consistecy).
* As the table grows, the scan slows.
* The more filters, the slower performance of a scan.

## Query vs Scan
 * Query is more efficient than Scan
 * Avoid using Scan on large table. 


