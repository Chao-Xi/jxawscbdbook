# **Quiz2 Storage**

### **Question 1**

Your big data application is taking a lot of files from your local on-premise NFS storage and inserting them into S3. As part of the data integrity verification process, the application downloads the files right after they've been uploaded. What will happen?

> S3 is eventually consistent only for DELETE or overwrite PUT

* The application will receive a 404 as S3 is eventually consistent 
* **The application will receive a 200 as S3 for new PUT is strongly consistent** 


### **Question 2**

You are gathering various files from providers and plan on analyzing them once **every month using Athena**, which must return the query results immediately. You do not want to run a high risk of losing files and want to minimise costs. Which storage type do you recommend?

* S3 General Purpose 
* **S3 Infrequent Access** 
* S3 One Zone Infrequent Access 
* S3 Glacier 

### **Question 3**

As part of your compliance as a bank, you must archive all logs created by all applications and ensure they cannot be modified or deleted for at least 7 years. Which solution should you use?

* S3 General Purpose with a Bucket Policy 
* **Glacier with a Vault Lock Policy** 
* Glacier with a Vault Access Policy 
* S3 Infrequent Access with a Bucket Policy 

### **Question 4**

You are generating thumbnails in S3 from images. Images are in the `images/` directory while thumbnails in the `thumbnails/` directory. After running some analytics, you realized that images are rarely read and you could optimise your costs by moving them to another S3 storage tiers. What do you recommend that requires the least amount of changes?


* Create two different buckets for images and thumbnails 
* Change the default storage class for the bucket to S3 Infrequent Access 
* Create a Lifecycle Rule for the entire bucket 
* **Create a Lifecycle Rule for the images/ prefix** 

### **Question 5**

In order to perform fast big data analytics, it has been recommended by your analysts in Japan to continuously copy data from your S3 bucket in us-east-1. How do you recommend doing this at a minimal cost?

* **Enable Cross Region Replication**
* Create an EC2 instance in us-east-1 and run `s3 sync` with a cron job 
* Create an EC2 instance in Japan and run `s3 sync` with a cron job 
* Use CloudFront 

### **Question 6**

Your big data application is taking a lot of files from your local on-premise NFS storage and inserting them into S3. As part of the data integrity verification process, you would like to ensure the files have been properly uploaded at minimal cost. How do you proceed?

* Download the files back onto your machine and compare the MD5 hash 
* **Compute the local ETag for each file and compare them with AWS S3's ETag** 
* Download the files back onto your machine and compare the SHA-256 hash 

### **Question 7**

Your application plans to have 15,000 reads and writes per second to S3 from thousands of device ids. Which naming convention do you recommend?

> you get about 3k reads per second per prefix, so using the device-id will help having many prefixes and parallelize your writes

* **`<device-id>/yyyy-mm-dd/....`** 
* `yyyy-mm-dd/<device-id>/....` 
* `mm-dd-yyyy/<device-id>/....` 
* `dd-mm-yyyy/<device-id>/....`

### **Question 8**

You are looking to have your files encrypted in S3 and do not want to manage the encryption yourself. You would like to have control over the encryption keys and ensure they're securely stored in AWS. What encryption do you recommend?

* SSE-C 
* **SSE-KMS** 
* SSE-S3 
* Client Side Encryption 
* TLS encryption 


### **Question 9**

Your website is deployed and sources its images from an S3 bucket. Everything works fine on the internet, but when you start the website locally to do some development, the images are not getting loaded. What's the problem?

* S3 Bucket Policies 
* **S3 CORS** 
* S3 ACLs 
* S3 Encryption 

### **Question 10**

What's the maximum number of fields that can make a primary key in DynamoDB?

> partition key + sort key

* 1
* 2
* 3
* 4

### **Question 11**

What's the maximum size of a row in DynamoDB ?

* 1KB
* **400KB**
* 1MB
* 400MB

###  **Question 12**

You are writing item of 8 KB in size at the rate of 12 per seconds. What WCU do you need?

> 8 * 12

* 12
* 24
* 48
* **96**

### **Question 13**

You are doing **strongly consistent** read of 10 KB items at the rate of 10 per second. What RCU do you need?

> 10 KB gets rounded to 12 KB, divided by 4KB = 3, times 10 per second = 30

* 100
* **30**
* 20
* 25

### **Question 14**

You are doing **12 eventually consistent reads** per second, and each item has a size of 16 KB. What RCU do you need?

> we can do 2 eventually consistent reads per seconds for items of 4 KB with 1 RCU
> 
> (12/2)*(16/4)=24

* 192
* 48
* **24**
* 12


### **Question 15**

We are getting a **ProvisionedThroughputExceededExceptions** but after checking the metrics, we see we haven't exceeded the total RCU we had provisioned. What happened?

>  remember RCU and WCU are spread across all partitions

* The metrics are slow to update 
* **We have a hot partition / hot key** 
* There's a bug in the code 

### **Question 16**

You are about to enter the Christmas sale and you know a few items in your website are very popular and will be read often. Last year you had a ProvisionedThroughputExceededException. What should you do this year?


* Increase the RCU to a very, very high value 
* **Create a DAX cluster** 
* Migrate the database away from DynamoDB to ElastiCache for the time of the sale 


### **Question 17**

You would like to react in real-time to users de-activating their account and send them an email to try to bring them back. The best way of doing it is to...

* Setup a trigger with SNS 
* Setup CloudWatch Events cron job that triggers a Lambda function who searches for account de-activations every 5 minutes 
* Enable Kinesis Streams 
* **Integrate Lambda with a DynamoDB stream** 

### **Question 18**

You would like to have DynamoDB automatically delete old data for you. What should you use?

* **Use TTL** 
* Use DynamoDB Streams
* Use DAX 
* Use a Lambda function 

### **Question 19**

You are looking to improve the performance of your RDS database by caching some of the most common rows and queries. Which technology do you recommend?

* Redshift 
* Athena 
* **ElastiCache** 
* EBS 
