# **Quiz7 Amazon ES** 

### **Question 1** 

How can you ensure maximum security for your Amazon ES cluster? 

* Bind with a VPC 
* Use security groups 
* Use IAM policies 
* Use access policies associated with the Elasticsearch domain creation 
* **All of the above** 

### **Question 2** 

As recommended by AWS, you are going to ensure you have dedicated master nodes for high performance. As a user, what can you configure for the master nodes? 

* **The count and instance types of the master nodes** 
* The EBS volume associated with the node 
* The upper limit of network traffic / bandwidth 
* All of the above. 


### **Question 3** 

Which are supported ways to import data into your Amazon ES domain? 

* Directly from an RDS instance
* **Via Kinesis, Logstash, and Elasticsearch's API's**
* Via Kinesis, SQS, and Beats 
* Via SOS, Firehose, and Logstash 

> Kinesis, DynamoDB, Logstash / Beats, and Elasticsearch's native API's offer means to import data into Amazon ES. 
> 
> **No SQS** 


### **Question 4** 

What can you do to prevent data loss due to nodes within your ES domain failing? 

* Raise a ticket with AWS support to have the ES launched in 2 or more regions at a time 
* Use the multi-AZ balancing feature 
* **Maintain snapshots of the Elasticsearch Service domain** 
* Enable serverless mode in Amazon ES 

> Amazon ES created daily snapshots to S3 by default, and you can create them more often if you wish. 

### **Question 5** 


You are going to setup an Amazon ES cluster and have it configured in your VPC. You want your customers outside your VPC to visualize the logs reaching the ES using Kibana. How can this be achieved? 

* Use a reverse proxy 
* Use a VPN 
* Use VPC Direct Connect 
* **Any of the above.** 
