# Uber Take Home Exercise
## Topics
### 1)	ETL model and Assumptions
### 2)  ETL Architecture
### 3)  Requirements
### 4)	Steps for Running/Deploying the application


1. Idea behind the ETL model and Assumptions:

a) Data Model:

My data model consists of three tables. Each of these tables have been extracted from the log file provided. The below image explains the column types and relationships between the tables. The Fact table has an ID column as auto increment which is the primary key of the table. The Date_Time and Dates columns have been extracted from the timestamp column in the log file provided. The vehicle and function dimensions have their primary keys as vehicle_id and function_id respectively. At this stage I am assuming the dimensions are not slowly changing dimensions but only contain details about the vehicles and functions. I have created the other columns in both the dimensions as examples to show how these dimensions can hold information about the vehicles and functions.



<img src="Uber_Assignment.PNG" width="700" height="350">


2) ETL Architecture:

a) Services leveraged:

I have created an ETL process using AWS S3, AWS Redshift and Databricks platforms.
I have used AWS S3 buckets as the source of the data. Databricks clusters are being used to extract and transform the data using python and spark apis. Finally, Redshift for loading the data in a warehouse, that holds the data. The code for the whole process is one single databricks notebook (python/ipynb file). This notebook integrates all the services together using different libraries in python and databricks.

b) Architecture diagram:

The python program extracts data stored in an S3 bucket. You need to spinup a Databricks cluster to run the code using the free service on the community edition. The S3 bucket is mounted on the Databricks cluster you are running your code on. You need to install the JDBC coonector for Redshift which is available as a jar file on the AWS website. I have provided the link and method of installation below in the requirements section. 

The data from the S3 bucket is loaded into a spark dataframe using the code and the transformation is performed on the Databricks cluster. After the transformation is complete the tables are created on the Redshift database you have assigned and the data is loaded to the tables. The first time you run the code, the tables are created and the data is loaded. Every other time when you run the code, the data is appended to the existing tables.

The diagram below explains the connections between S3, Databricks and Redshift.

                            ┌───────┐
       ┌───────────────────>│  S3   │<─────────────────┐
       │    IAM or keys     └───────┘    IAM or keys   │
       │                        ^                      │
       │                        │ IAM or keys          │
       v                        v               ┌──────v────┐
┌────────────┐            ┌───────────┐         │┌──────────┴┐
│  Redshift  │            │  Spark    │         ││   Spark   │
│            │<──────────>│  Driver   │<────────>| Executors │
└────────────┘            └───────────┘          └───────────┘
               JDBC with                  Configured
               username /                     in
               password                     Spark
        (SSL enabled by default)
        
  





