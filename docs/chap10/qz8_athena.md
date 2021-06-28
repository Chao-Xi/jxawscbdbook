# **Quiz8 Amazon Athena**

### **Question 1** 


As a Big Data analyst, you need to query/analyze data from a set of CSV files stored in S3. Which of the following serverless services helps you with this? 

* AWS Glacier 
* AWS EMR 
* **AWS Athena** 
* AWS Redshift 


### **Question 2** 

What are two columnar formats supported by Athena 

* GZip and LZO 
* AVRO and Parquet 
* AVRO and ORC 
* **Parquet and ORC** 

### **Question 3** 

Your organization is querying JSON data stored in S3 using Athena, and wishes to reduce costs and improve performance with Athena. What steps might you take? 

* Reduce the server count for Athena 
* **Convert the data from JSON to ORC format, and analyze the ORC data with Athena **
* Convert the data from JSON to AVRO format, and analyze the AVRO data with Athena 
* Enable slow logging for Athena 


> "Slow logs" is a feature in Amazon Elasticsearch Service, but it's not a thing with Athena. 
> 
>  Athena is serverless; this isn't something you control. 
> 
> **Using columnar formats such as ORC and Parquet can reduce costs 30-90%, while improving performance at the same time.**


### **Question 4**

When using Athena, you are charged separately for using the AWS Glue Data Catalog. True or False ? 

* **True** 
* False 


### **Question 5** 

Which of the following statements is NOT TRUE regarding Athena pricing? 

* Amazon Athena charges you for cancelled queries 
* **Amazon Athena charges you for failed queries** 
* You will get charged less when using a columnar format 
* Amazon Athena is priced per query and charges based on the amount of data scanned by the query 