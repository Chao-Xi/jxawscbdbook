# **Quiz6 Kinesis Analytics** 

### **Question 1** 

From which sources can the input for Kinesis analytics be obtained ? 

* MySQL and Kinesis Data Streams 
* DynamoDB and Kinesis Firehose deliver streams 
* **Kinesis data streams and Kinesis Firehose delivery streams** 
* Kinesis Data Streams and DynamoDB 


**Kinesis Analytics can only monitor streams from Kinesis, but both data streams and Firehose are supported.** 


### **Question 2**


After real-time analysis has been performed on the input source, where may you send the processed data for further processin ? 

* Amazon S3 
* Redshift 
* Athena 
* **Kinesis Data Stream or Firehose** 
* All of the above 

> While you might in turn connect S3 or Redshift to your Kinesis Analytics output stream, Kinesis Analytics must have a stream as its input, and a stream or Lambda function as its output. 

### **Question 3**

If a record arrives late to your application during stream processing, what happens to it? 

* **The record is written to the error stream**
* The record is processed with the late timestamp 
* The record is discarded entirely 
* None of the above 

> **Application error stream:**
> 
> Certain records like a type **mismatch** or **late arrival** wiil be written out to the erro stream. 

### **Question 4**
 
You have heard from your AWS consultant that Amazon Kinesis Data Analytics elastically scales the application to accommodate the data a-IVUULpUa. What though is defaultfault capacity of the processing application in terms of memory? 

* 48GB 
* 12GB 
* 24GB 
* **32GB**

Kinesis Data Analytics provisions capacity in the form of Kinesis Processing Units (KPU). **A single KPU provides you with the memory (4 GB) and corresponding computing and networking. The default limit for KPUs for your application is eight**. 

### **Question 5**

You have configured data analytics and have been streaming the source data to the application. You have also configured the destination correctly. However, even after waiting for a while, you are not seeing any data come up in the destination. What might be a possible cause? 


* Issue with IAM role 
* Mismatched name for the output stream 
* Destination service is currently unavailable 
* **Any of the above** 

