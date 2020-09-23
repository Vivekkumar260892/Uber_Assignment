# Uber Take Home Exercise
## Topics
### 1)	Idea behind the ETL model and Assumptions
### 2)  Requirements
### 3)	Steps for Running/Deploying the application


1. Idea behind the ETL model and Assumptions:

a) Data Model:
My data model consists of three tables. Each of these table have been extracted from the log file provided. The below image explains the column types and relationshipd between the tables. The Fact table has an ID column as auto increment which is the primary key of the table. The vehicle and function dimanesions have their primary keys as vehicle_id and function_id respectively.



I have created an ETL process using AWS S3, AWS Redshift and Databricks platforms.
I have used AWS S3 buckets as the source of the data, Databricks clusters to process and transform the data using python and spark apis. Finally, Redshift as the data warehouse, that holds the data. 
