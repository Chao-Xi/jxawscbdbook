# **L2 AWS Big Data Instances**

## **1、Instance Types for Big Data (D, B, G, R)**

### **1-1 General Purpose: T2,T3, M4, M5** 

### **1-2 Compute Optimized:  C4, C5**

**Batch processing**, Distributed analytics, **Machine / Deep Learning Inference** 

### **1-3 Memory Optimized: R4, R5, X1 , Z1d** 

High performance database, **In memory database**, Real time big data analytics 

### **1-4 Accelerated Computing: P2, P3, G3, F1** 

GPU instances, **Machine or Deep Learning**, High Performance Computing 

### **1-5 Storage Optimized: H1 , 13, D2**

**Distributed File System (HDFS)**, NFS, **Map Reduce, Apache Kafka**, **Redshift** 


> Tensorflow for machine learning and MXNet for accelerated computing:  P2, P3, G3
> 
>  Batch processing for compute optimized


## **2、EC2 in Big Data** 

### **2-1 On demand, Spot & Reserved instances:** 

* Spot can tolerate loss, low cost => checkpointing feature (ML, etc) 
* Reserved: long running clusters, databases (over a year) 
* On demand: remaining workloads 

### **2-2 Auto Scaling:** 

* Leverage for EMR, etc 
* Automated for DynamoDB, Auto Sca ing Groups, etc... 

### **2-3 EC2 is behind EMR** 

* Master Nodes 
* Compute Nodes (contain data) + Tasks Nodes (do not contain data) 
