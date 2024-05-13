1. Usecase 1:
     Given jioTV data of customers profile details, containing two tables one for inidividual data and another for corporate data. I have joined the two tables based on customer id
     and written to csv using spark and the csv stored in hdfs is sent to SFTP server using NiFi flow
     Made hive script to create external table on top of csv
     Written shell scripts to run the spark code and hive scripts
     Created and scheduled dags to create table once, and update the table daily
     Generated and analysed stats of spark-jobs in production and checked the health of job using yarn, wxm and grafana

2. Usecase 2:
     Given jio Cinema data, exploded the data in a json column into multiple columns using UDFs in spark, and created table on top of it and extracted the list of top 3 actors, top 3 directors using rank in sql

3. Usecase 3:
     Read data from kafka topic using spark as key-value pairs, extracted the values in json format and splitted into columns and stored into hdfs location.

4. Usecase 4:
     A table in jiomedia has less than 100 rows. So it has to be saved in mysql server instead of hive. Made a connection request to mysql server, created table there and inserted data into it from dataframe.
