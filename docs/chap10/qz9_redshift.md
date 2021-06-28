# **Quiz9 Amazon Redshift**

### **Question 1**

You are working as Big Data Analyst of a data warehousing company. The company uses RedShift clusters for data analytics. **For auditing and compliance purpose**, you need to monitor API calls to 
RedShift instance and also provide secured data. 

Which of the following services helps in this regard ? 

* **CloudTrail logs** 
* Cloud Watch logs 
* Redshift Spectrum 
* AmazonMQ 

### **Question 2** 

You are working as a Big Data analyst of a Financial enterprise which has a large data set that needs to have columnar storage to reduce disk IO. It is also required that the data should be queried fast so as to generate reports. Which of the following service is best suited for this scenario? 

* DynamoDB 
* RDS 
* Athena 
* **Redshift** 


### **Question 3** 

You are working for a data warehouse company that uses Amazon RedShift cluster. It is required that VPC flow logs is used to monitor all COPY and UNLOAD traffic of the cluster that moves in and out of the VPC. Which of the following helps you in this regard ? 

* By using RedShift Spectrum 
* **By enabling Enhanced VPC routing on the Amazon Redshift cluster** 
* By using RedShift WLM 
* By enabling audit logging in the Redshift cluster 

### **Question 4** 

You are working for a data warehousing company that has large datasets (20TB of structured data and 20TB of unstructured data). They are planning to host this data in AWS with unstructured data storage on S3. At first they are planning to migrate the data to AWS and use it for basic analytics and are not worried about performance. Which of the following options fulfills their requirement? 

* **node type ds2.xlarge** 
* node type ds2.8xlarge 
* with node type dc2.8xlarge 
* node type dc2.xlarge 


> Since they are not worried about performance, storage (ds) is more important than computing power (dc,) and expensive 8xlarge instances aren't necessary. 


### **Question 5** 

Which of the following services allows you to directly run SQL queries against exabytes of unstructured 
data in Amazon S3? 

* Athena 
* **Redshift Spectrum** 
* Elasticache 
* RDS 
