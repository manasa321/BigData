# Hadoop #

Hadoop cluster  fits best under the situation of parallel computation for processing the data.

Master, slave, client nodes are in hadoop which loads and stores data in HDFS.

## Modules ##

The project includes these modules:

**Hadoop Common:** The common utilities that support the other Hadoop modules.   
**Hadoop Distributed File System (HDFS™):** A distributed file system that provides high-throughput access to application data.  
**Hadoop YARN:** A framework for job scheduling and cluster resource management.  
**Hadoop MapReduce:** A YARN-based system for parallel processing of large data sets.  

## YARN: ##
A resource management platform that allows multiple data processing engines like real-time streaming, batch processing, and interactive SQL, to run and process data stored in HDFS.

## HDFS ##
HDFS splits files into blocks and sends them across various nodes in form of large clusters. Also in case of a node failure, the system operates and data transfer takes place between the nodes which are facilitated by HDFS.
HDFS aims to move the computation to where the data resides rather than moving the data to the computation.
Data is stored in distributed manner i.e. various Datanodes are responsible for storing the data.
**Why We Need DFS?**  

You might be thinking that we can store a file of size 30TB in a single system then why we need this DFS. This is because the disk capacity of a system can only increase up to an extent. If somehow you manage the data on a single system then you’ll face the processing problem, processing large datasets on a single machine is not efficient. 

Let’s understand this with an example. Suppose you have a file of size 40TB to process. On a single machine, it will take suppose 4hrs to process it completely but what if you use a DFS(Distributed File System). In that case, as you can see in the below image the File of size 40TB is distributed among the 4 nodes in a cluster each node stores the 10TB of file. As all these nodes are working simultaneously it will take the only 1 Hour to completely process it which is Fastest, that is why we need DFS. 

**Local File System Processing:**
![image](https://github.com/manasa321/BigData/assets/56963182/348d1ab0-5b68-40bd-ac02-74e3963dbcc5)

**Distributed File System Processing:**

![image](https://github.com/manasa321/BigData/assets/56963182/2947e051-d453-4433-8ed9-d27ba7bce1f0)

##Hadoop Daemons##

It has Name node and Data Node for storing the data

**NameNode:** Acts as a Master Node. It stored metadata such as transaction logs, name of files, size of files, (Block number, Block id) information of data nodes. Namenode instructs the DataNodes with the operation like delete, create, Replicate, etc. 

**Data Node:** Works as slave nodes which are used to store data in hadoop. Data nodes range from 1 to 500. More the data nodes, more data can be stored in hdfs. 




