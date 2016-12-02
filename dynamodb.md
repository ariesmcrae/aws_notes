# DynamoDB

## Facts
* Single-diti millisecond latency
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

## Lab
* Give EC2 IAM role of AmazonDynamoDBFullAccess.
