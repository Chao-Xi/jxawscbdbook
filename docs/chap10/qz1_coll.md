# **Quiz1 Collection**

### **Question 1**

You are accumulating data **from IoT devices** and you must send data within **10 seconds to Amazon ElasticSearch service**. That data should also be consumed by other services when needed. Which service do you recommend using? 

* **Kinesis Data Streams** 
	* *Steams (click streams, IoT devices and metrics, logs)*
	* *Great for real-time big data*
* Kinesis Data Firehose 
* SQS 
* Database Migration Service 


### **Question 2**

You need a managed service that can deliver data to Amazon S3 and **scale automatically for you**. You want to be **billed only for the actual usage of the service and be able to handle peak loads**. Which service do you recommend? 

* Kinesis Data Streams 
	* _Auto Scaling is not a native feature of Kinesis Data Streams_
* **Kinesis Data Firehose** 
	* *Load data into Redshift Amazon S3 / ElasticSearch / Splunk*
	* *Automatic scaling*
	* *Pay for the amount of data going through Firehose*
* SQS 
* Kinesis Analytics 


### **Question 3**


You are **sending a lot of 100B data** records and would like to ensure you can use Kinesis to receive your data. What should you use to ensure optimal throughput, that has **asynchronous features** ? 

* Kinesis SDK 
* **Kinesis Producer Library** 
	* *Synchronous or Asynchronous API (better performance for async)*
	* *Batching (both turned on by default) — increase throughput, decrease cost*
* Kinesis Client Library 
* Kinesis Connector Library 
* Kinesis Agent 


> (Through batching (collection and aggregation), we can achieve maximum throughput using the KPL. KPL is also supporting an asynchronous API 


### **Question 4**

You would like to collect log files in mass from your Linux servers running on premise. **You need a retry mechanism embedded and monitoring through CloudWatch. Logs should end up in Kinesis**. What will help you accomplish this? 

* Kinesis SDK 
* Kinesis Producer Library 
* **Kinesis Agent** 
	* *Monitor Log files and sends them to Kinesis Data Streams*
	* *Emits metrics to CloudWatch for monitoring*
* Direct Connect 

### **Question 5** 

You would like to perform **batch compression** before sending data to Kinesis, in order to **maximize the throughput**. What should you use? 

* Kinesis SDK 
* Kinesis Producer Library Compression Feature 
* **Kinesis Producer Library + Implement Compression Yourself** 
	* *Kinesis Producer Library (KPL): Compression must be implemented by the user* 


### **Question 6** 

You have **10 consumers applications** consuming concurrently from one shard, in classic mode by issuing Getrecords() commands. what is the the average latency for consuming these records for each application? 

* 70 ms 
* 200 ms 
* 1 sec 
* **2 sec** 
	* **Maximum of 5 GetRecords API calls per shard per second**
	* **10 / 5 * 2 = 2**


> You can issue up to 5 GetRecords API calls per second, so it'll take 2 seconds for each consuming application betore they can issue their next call 

### **Question 7** 

You have 10 consumers applications consuming **concurrently from one shard, in enhanced fan out mode**. What is the average latency for consuming these records for each application? 

* **70 ms** 
	* *That means 20 consumers will get 40MB/s per shard aggregated* 
	* *Reduce latency (~70 ms)*
* 200 ms 
* 1 sec 
* 2 sec 


> here, no matter how many consumers you have, in enhanced fan out mode, each consumer will receive 2MB per second of throughput and have an average latency of 70ms. 


### **Question 8**

You would like to have data delivered in **near real time** to Amazon ElasticSearch, and the **data delivery to be managed by AWS**. What should you use? 

* Kinesis Client Library (KCL) 
* Kinesis Connector Library 
* **Kinesis Firehose** 
	* *Near Real Time (60 seconds latency minimum for non full batches)*
	* *Fully Managed Service, no administration*

 

### **Question 9** 

You are consuming from a Kinesis stream with 10 shards that receives on average 8 MB/s of data from various producers using the KPL. You are therefore using the KCL to consume these records, and **observe through the CloudWatch metrics that the throughput is 2 MB/s, and therefore your application is lagging**. What's the most likely root cause for this issue? 

* You need to split shards some more 
* There's a hot partition 
* Cloudwatch is displaying the average throughput metric, not the aggregate one 
* **Your DynamoDB table is under-provisioned** 
	* Leverages DynamoDB for coordination and checkpointing (one row per shard) 
		* Make sure you provision enough WCU / RCU
		* Or use On-Demand for DynamoDB
		* **Otherwise DynamoDB may slow down KCL**


> Because it's under provisioned, checkpointing does not happen fast enough and results in a lower throughput for your KCL based application. Make sure to increase the RCU / WCU 

### **Question 10**

You would like to increase me capacity of your **Kinesis streams**. What should you do? 

* **Split Shards** 
	* *Can be used to increase the Stream capacity ( 1 MB/s data in per shard)*
* Merge Shards 
* Turn on Auto Scaling 
	* _Auto Scaling is not a native feature of Kinesis data streams_


### **Question 11**

Which of the following statement is wrong? 

* Spark Streaming can write to Kinesis Data Streams 
* **Spark Streaming can read from Kinesis Data Firehose** 
* Spark Streaming can read from Kinesis Data Streams 

### **Question 12** 

Which of tho follnwing Kinesis Data Firehose does not write?

* S3 
* Redshift 
* **DynamoDB** 
* ElasticSearch 
* Splunk 
	* **Load data into Redshift Amazon S3 / ElasticSearch / Splunk** 

### **Question 13** 

You are looking to decouple jobs and **ensure data is deleted after being processes**. Which technology would you choose? 

* Kinesis Data Streams 
* Kinesis Data Firehose 
* **SQS** 
	* **Process the message within the visibility timeout**
	* **Delete the message using the message ID & receipt handle**

> That means that basically when you have SQS your consumers will poll messages and you consumers will process these messages and then delete them from the SQS Queue

### **Question 14** 

You are collecting data from loT devices at scale and would like to forward that data into Kinesis Data Firehose. How should you proceed? 

* **Send that data into an loT topic and define a rule action** 
* Use enhanced fanout for the loT topic and send that data into Kinesis Data Streams 
* Create an SNS topic, send the IoT data there and use AWS Lambda 
* Send that data into an loT topic and use device shadow 

### **Question 15** 

Which protocol is not supported by the IoT Device Gateway? 

* MQTT 
* Websockets 
* HTTP 1.1 
* **FTP** 


### **Question 16** 


You would like to control the target temperature of your room using an IoT thing thermostat. How can you change its state for target temperature even in the case it's temporarily offline? 

* Send a message to the loT broker every 10 seconds until it is acknowledged by the loT thing 
* Use a rules actions that triggers when the device comes back online 
* **Change the state of the device shadow** 
* Change its metadata in the thing registry 

> That's precisely the purposes of the device shadow, which gets synchronized with the device when it comes back online 


### **Question 17**

You are looking to continuously replicate a MySQL database that's on premise to Aurora. Which service will allow you to do so securely? 

* AWS Direct Connect 
* **Database Migration Services** 
* AWS Lambda 
* Kinesis Data Streams 


> DMC is fully secure 


### **Question 18**


You have setup Direct Connect on one location to ensure your traffic into AWS is going over a private network. You would like to setup a failover connection, that must be as reliable and as redundant as possible, as you cannot afford to be down for too long. What backup connection do you recommend? 

* Another Direct Connect setup 
* **Site to Site VPN**
* Client Side VPN 
* Snowball Connection 


> although this is not as private another Direct Connect setup, it is definitely more reliable as it leverage the public web. it is the correct answer


### **Question 19**

You would like to transfer data in AWS in less than two days from now. What should you use? 

* Setup Direct Connect  
* **Use the Public Internet** 
* Use AWS Snowball 
* Use AWS Snowmobile 