![image](https://github.com/manasa321/BigData/assets/56963182/bedbf60e-7bc0-438f-9e92-89cc7ff45eba)1. Usecase 1:
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


# Course Projects #

## Compiler Design Course
(Aug’21-Nov’22) ##

```
1. Developed a 5-pass compiler in Java to translate MiniJava programs into progressively lower-level representations, culminating in MIPS assembly language.
2. Implemented type-checking, intermediate code generation, and optimized register allocation within the compiler.
```


## Computer Architecture 
(Jan’21-May’21) ##
```
1. Simulated a 5-stage scalar pipelined processor based on RISC architecture using C++.
2. Utilized multithreading to parallelize the simulation of each stage, enhancing overall execution speed.
3. Implemented a single-level cache with Random, LRU, and Pseudo LRU replacement policies.
```

## Smart Sensing for IoT (Jan-May’23) ##
```
1. Developed a heart rate measurement system using smartphone-based photoplethysmography: Captured and analyzed video data post various physical activities to calculate heart rate. Determined optimal thresholds for each activity and generated ROC curves and histograms to validate results.

2. Implemented an occupancy detection system using ESP32 devices and Channel State Information (CSI) data: Collected CSI data in scenarios involving 0-4 people between a transmitter and receiver under static and dynamic conditions. Processed CSI amplitude data into images, applied Singular Value Decomposition (SVD) for dimensionality reduction, and utilized k-means clustering to classify real-time data as vacant/non-vacant and static/dynamic.
```

## Pattern Recognition& Machine learning(jul-nov’22) ##
```

```


