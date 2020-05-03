# Project 2: Tracking User Activity

Project 2: Tracking User Activity
Vaibhav Beohar - Spring w205 - Section 4
==============================================

Following project is an attempt created by a hypothetical employee at an ed-tech firm that does the following:

- creates a topic called "assessments" on Kafka
- publishes assessments by various users of the ad tech firm
- allows data scientists working at the ad tech firms' customers to run queries on the asessements topic

The approach taken by the project is as follows:

- Create Kafka topic for publishing-subscribing topic assessment for production-consumption
- Create a Spark base execution engine, to perform ETL, use of programming languages such as Python, providing in-memory execution of data using Spark SQL and store the massively parallel RDD (Robust Distributed Dataset) to allow us to store data on memory in a transparent manner and to retain it on disk as required
- Finally save the RDD files in the HDFS base file system for Hadoop


Following files have been provided as part of the submission of this project: 

- docker-compose.yml - File that contains initialization configuration set up for pipelines for Kafka, Hadoop etc.  
- Project_2.ipynb - Final primary submission file with commands listed out and work done by each week 
- vbeohar_commands_by_weeks.txt - Listing of all commands instructed by weeks 6, 7, 8 for this project
- vbeohar-history.txt - History file of all commands executed on the GCP instance
- README.md -- File listing the initial requirements of the project
