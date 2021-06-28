# **AWS Certified Data Analytics Specialty Practice Exam**


### **Question 1** 

What are THREE ways in which **EMR integrates Pig with Amazon S3**? 

* **Submitting work from the EMR console using Pig scripts stored in S3 
(Correct)** 
* **Loading custom JAR files from S3 with the REGISTER command (Correct)**
* Integration with AWS Glue to infer schemas on S3 data 
* **Directly writing to HCatalog tables in S3 (Correct)** 
* Importing permissions from S3 buckets for use in your Pig Latin scripts 


> **Explanation** You can configure **EMRFS, backed by S3, as your data store in Pig**, which allows it to read and write to S3 as it would with HDFS. 


### **Question 2**

An organization has a large body of **web server logs stored on Amazon S3**, and **wishes to quickly analyze their data using Amazon Athena**. Most queries are operational in nature, and are limited to a single day's logs.

How should the log data be prepared to provide the most performant queries in Athena, and to minimize costs? 

* **Convert the data into Apache Parquet format, compressed with Snappy, stored in a directory structure of `year=XXXX/month=XX/day=XX/`   (Correct)**
* Convert the data into AVRO format, with filenames that may be sorted by date 
* Convert the data into Apache ORC format, uncompressed, and rotate their LI directories daily 
* Compress the log data with gzip, and rotate their directories daily 


> **Explanation** Athena works best with columnar data; Parquet and ORC are both examples of columnar formats (Gzip and AVRO are not.) 
> 
> Compressing the data will allow them to be transferred more efficiently, and partitioning it using the "partition key=value" format in directory names further allows Athena to process only the data it needs. 


### **Question 3:**

A large news website needs to produce personalized recommendations for articles to its readers, by training a machine learning model on a daily basis using historical click data. **The influx of this data is fairly constant, except during major elections when traffic to the site spikes considerably**. 

Which system would provide the most cost-effective and reliable solution? 

* Publish click data into Amazon Elasticsearch using Kinesis Firehose, and query  the Elasticsearch data to produce recommendations in real-time. 
* Publish click data into Amazon S3 using Kinesis Streams, and process the data in real time using Splunk on an EMR cluster with spot instances added as needed.Publish the model's results to DynamoDB for producing recommendations in real-time. 
* **Publish click data into Amazon S3 using Kinesis Firehose, and process the data nightly using Apache Spark and MLLib using spot instances in an EMR cluster. Publish the model's results to DynamoDB for producing recommendations in real-time. 
(Correct)**
* Publish click data into Amazon S3 using Kinesis Firehose, and process the data nightly using Apache Spark and MLLib using reserved instances in an EMR cluster. Publish the model's results to DynamoDB for producing recommendations in real-time.

> **Explanation**
> 
>  The use of spot instances in response to anticipated surges in usage is the most cost-effective approach for scaling up an EMR cluster, which rules out "Publish click data into Amazon S3 using Kinesis Firehose, and process the data nightly using Apache Spark and MLLib using reserved instances in an EMR cluster. Publish the model's results to DynamoDB for producing recommendations in real-time.". 
> 
> Kinesis streams is over-engineering because we do not have a real-time streaming requirement, ruling out "Publish click data into Amazon S3 using Kinesis Streams, and process the data in real time using Splunk on an EMR cluster with spot instances added as needed. Publish the model's results to DynamoDB for producing recommendations in real-time." 
> 
> "Publish click data into Amazon Elasticsearch using Kinesis Firehose, and query the Elasticsearch data to produce recommendations in real-time." doesn't make sense because Elasticsearch is not a recommender engine. 
 
### **Question 4:**

Of the 4 four types of identity principals for authentication supported by AWS IoT, which one is commonly used by mobile applications? 

* IAM users, groups and roles 
* X.509 certificates 
* Federated Identities  
* **Cognito Identities (Correct)**

> **Explanation** 
> 
> For IoT mobile applications, the standard is to leverage Cognito. 

### **Question 5:** 

An e-commerce company wishes to assign product categories, such as sporting goods or books, to new products that have no category assigned to them. The company has a large corpus of existing product data with manually assigned categories in place. **They wish to use their existing data to predict categories on new products**, based on other attributes of the products such as its keywords and seller ID, using Amazon Machine Learning. 

Which type of machine learning model would they use? 

* Binary classification model 
* **Multi-class classification model  (Correct)**
* Regression model 
* Unary classification model 

> **Explanation** 
> 
> Since you are trying to **predict categorical data and there are more than two categories, this is a multi-class classification model**. Unary classification isn't really a thing. Under the hood, Amazon ML would use a logistic regression to implement a classification model. 

### **Question 6:**

You are looking to reduce the latency down from your Big Data processing job that **operate in Singapore but source data from Virginia**. The Big Data job must always operate against the latest version of the data. What do you recommend? 


* **Enable S3 Cross Region Replication (Correct)**
* Install a CloudFront distribution on top of your S3 bucket
* Use S3 Transfer Acceleration 
* Create a Data Pipeline job to transfer the data regularly between two S3 buckets located in different regions 

> **Explanation** 
> 
> Here to reduce the latency you must move the data to another S3 bucket. The DataPipeline job may work but won't be able to replicate the latest data continuously, and CloudFront will cache some data and may provide outdated data to the Big Data Job. S3 Transfer acceleration will not help. Here, you must enable S3 Cross Region Replication 

### **Question 7:** 

You are deploying your web servers being a Load Balancer. The Load Balancer is in a public subnet and the web servers sit in a private subnet. For security reasons, the private subnet does not have access to internet and you would like to ensure the web servers within this subnet have access to DynamoDB. What do you recommend? 

* Enable Direct Connect between your VPC and DynamoDB 
* Create an Internet Gateway in the public subnet 
* Create a DynamoDB table within your VPC and attach a security group to it LI authorizing traffic from your EC2 instances. 
* **Provision a VPC Endpoint Gateway (Correct)**


> **Explanation** 
> 
> **An internet gateway will work but will break the security in place**. Direct Connect only helps connecting on premise data centers to AWS VPC. DynamoDB tables cannot be provisioned within a VPC. So you need to create a VPC Endpoint of type Gateway (please note they're not Interfaces, they're gateway). 

### **Question 8:** 

A financial services company has a large, secure data lake stored in Amazon S3. They wish to analyze this data using a variety of tools, including Apache Hive, Amazon Athena, Amazon Redshift, and Amazon QuickSight. 

How should they connect their data and analysis tools in a way that minimizes costs and development work? 

* Use the AWS Database Migration Service to load the S3 data into an Amazon Aurora database, and use replication to keep the data in sync. Connect Hive, Athena, Redshift, and QuickSight to the Aurora database. 
* Write an Apache Spark script on EMR to transform and load the S3 data nightly into Amazon Redshift. Connect Hive, Athena, and Quicksight to the Redshift cluster. 
* Write an Apache Spark script on EMR to transform the S3 data into a Hive database on a nightly basis, connect Redshift to the Hive repository, and connect Athena and QuickSight to Redshift. 
* **Run an AWS Glue Crawler on the data lake to populate a AWS Glue Data Catalog. Share the glue data catalog as a metadata repository between Athena, Redshift, Hive, and QuickSight.  (Correct)**


> **Explanation** 
> 
> AWS Glue crops up a lot on the exam. **Knowing that Glue can be used to connect to Athena, Redshift, and Quicksight - as well as being used as a Hive metastore -is key to understanding this question**. The other options are unnecessarily complex and require development work that could be avoided with Glue. 


### **Question 9:** 

You are working for a data warehouse company that uses Amazon RedShift cluster. For security reasons, it is required that VPC flow logs should be analyzed by Athena to monitor all COPY and UNLOAD traffic of the cluster that moves in and out of the VPC. Which of the following helps you in this regard ? 

* Use Redshift WLM 
* Use Redshift Spectrum 
* By enabling audit logging in Redshift cluster 
* **Use Enhanced VPC Routing  (Correct)**

> **Explanation** 
> 
> Enhanced VPC Routing forces Redshift to use the VPC for all COPY and UNLOAD commands, which in turn will help us make sure that all that traffic appears on the VPC Flow logs. 

### **Question 10**

Users of your Redshift cluster include analysts running complex, long-running queries as well as automated systems running short, **transactional read-only queries. During peak usage times, your transactional queries are timing out while the analysts are running their jobs**. What would be the simplest solution to this problem? 


* Use Automatic WLM with concurrency scaling
* Resize the cluster with Elastic Resize 
* **Use Short Query Acceleration (SQA)   (Correct)**
* Use Manual WLM with concurrency scaling 

> **Explanation** 
> 
> SQA can be used in place of WLM as a simple way to ensure short queries are **not scheduled behind longer ones**. 

### **Question 11**

You are running a Glue ETL job on a schedule to transform new log data from your webservers stored in S3. **What is the simplest approach for ensuring data is not re-processed in subsequent job runs**? 

* Delete data from S3 once it is processed 
* **Use job bookmarks    (Correct)**
* Enable the "data tracking" feature in Glue 
* Use a DynamoDB table to track where each job left off 

> **Explanation** 
> 
> Job bookmarks are made for this use case. The "data tracking" feature doesn't exist, and the other options are more complex. 

### **Question 12**

You are tasked with using **Hive on Elastic MapReduce to analyze data that is currently stored in a large relational database**. 

Which approach could meet this requirement? 

* Extract the database into csv files in Amazon S3, and point your EMR file systpm to that S3 bucket 
* Use AWS Glue to create a Hive metastore used by your EMR cluster 
* **Use Apache Sqoop on the EMR cluster to copy the data into HDFS (Correct)**
* Use Apache Flume to stream data from the database into HDFS 

> **Explanation** 
> 
> Sqoop is an open-source system for transferring data between Hadoop and relational databases. 
> 
> Flume is intended for real-time streaming applications, Glue is intended for use with S3, and you can't direct EMRFS to arbitrary S3 buckets. 


### **Question 13**

Your management wants a dashboard to **monitor current revenue against their annual revenue goal**. Whick Quicksight visualization would be most appropriate? 

* **KPI**
* Donut Chart 
* Line Chart
* Pie Chart 

> **Explanation** 
> 
> KPI, or Key Performance Indicator, is a newer visualization in Quicksight that lets you visualize a comparison between a key value and its target value. 

### **Question 14**

A company wishes to copy 500GB of data from their **Amazon Redshift cluster into an Amazon RDS PostgreSQL database**, in order to have both columnar and row-based data stores available. **The Redshift cluster will continue to receive large amounts of new data every day that must be kept in sync with the RDS database**. 

What strategy would be most efficient? 

* Use the Amazon Database Migration Service to sync the two databases using replication 
* Use a materialized view to cache data between the databases, refreshing it periodically using Amazon Lambda 
* **Copy data using the dblink function into PostgreSQL tables (Correct)** 
* Use AWS Glue to allow both databases to share a common metadata store 

> **Explanation** 
> 
> **Dblink allows you to offload queries in Redshift to another database entirely. A materialized view could work for this, but it will always copy from the beginning of the table**, and not just handle what has changed since the last incremental update. Read through https://amzn.to/2fraaHv if this question confused you. 

### **Question 15**

Your company collects data from various sources into Kinesis and the stream is delivered using Kinesis Data Firehose into S3. Once in S3, your data scientist team uses Athena to query the most recent data, and usage has shown that after a month, the team queries the data less and less, an**d finally after two months does not use it. For regulatory reasons, it is required to keep all the data for 5 years and no one should be able to delete it**. What do you recommend? (select two) 
after 60 days. 


* Create a lifecycle rule to migrate the data to S3 IA after 30 days and Glacier 
* **Implement a Glacier Vault Lock Policy (Correct)**
* Implement a Glacier Vault Access Policy 
* Create a lifecycle rule to migrate the data to S3 Athena one day 1 and S3 Athena IA after 30 days. 
* **Create a lifecycle rule to migrate all the data to S3 IA after 30 IA days and delete the data after 60 days. Create a rule to have a replica of all source data into Glacier from the first day.  (Correct)**


> **Explanation** 
> 
> S3 Athena is not a storage class. Data should be moved to S3 IA after 30 days. If the data is moved to Glacier after 60 days, then there are no guarantees for it not to be deleted by anyone for the first 60 days. Hence a replica of the data should be delivered to Glacier right away. **Finally, to prevent deletion in Glacier, you must use a Glacier Vault Lock Policy**. 


### **Question 16:**

A user or application has been changing configuration on your production S3 bucket and you would like to understand who did this. What do you recommend? 

* Analyze the S3 access logs with Athena 
* Use CloudTrail 
* Use the IAM action logs 
* Write a custom S3 bucket policy 

> **Explanation** 
> 
> Very simply, we're looking at searching through API calls done on your account, which CloudTrail was made for. 

### **Question 17:**

A hospital monitoring sensor data from heart monitors wishes to **raise immediate alarms** if an anomaly in any individual's heart rate is detected. Which architecture meets these requirements in a **scalable manner**? 

* Publish sensor data into S3, and use Kinesis Firehose to publish the data into a Spark Streaming application that detects anomalies and raises alarms. 
* Publish sensor data into a Kinesis data stream, and route the data into a custom application on an EC2 instance that analyzes the data for anomalies and sends out alarms as needed. 
* **Publish sensor data into a Kinesis data stream, and create a Kinesis Data Analytics application using `RANDOM_CUT_FOREST` to detect anomalies. When an anomaly is detected, use a Lambda function to route an alarm to Amazon SNS. (Correct)**
* Publish sensor data into S3, and use AWS Glue to query the data using Amazon Redshift Spectrum. Run a periodic script to query the data for anomalies using SQL and raise alarms when needed
 
> Explanation 
> 
> **`RANDOM_CUT_FOREST` is a function in Kinesis Data Analytics intended for anomaly detection.** **By using serverless services such as Kinesis, Lambda, and SNS we ensure the scalability of this system, and the choice of Kinesis Streams instead of Firehose ensures real-time delivery of the data**. 



### **Question 18:** 

You are launching an EMR cluster and plan on running custom python scripts that will end up invoking **custom Lambda functions deployed within your VPC**. How can you ensure the EMR cluster has the right to invoke the functions? 
—taws/credentials file 

* Create an IAM user and put the credentials into the `~/.aws/credentials` file
* **Create an IAM role and attach it to the EMR instances (Correct) **
* Attach a VPC Endpoint to Lambda and map a route to EMR 
* Create an AWS Lambda policy and authorize the EMR cluster security groups

> **Explanation** 
> 
> As EMR is made of EC2 instances, the best and most secure way for them to be **allowed to invoke a Lambda function is to attach IAM roles**. There's no Lambda policy or VPC Endpoint that can help for that matter. 



### **Question 19:**

You would like to process data coming from IoT devices, and processing that date takes approximately 2 minutes per data point. You would also like to be able to scale in terms of number of processes that will consume that data, based on the load your are receiving, and no ordering constraints are required. What do you recommend? 

* Define an IoT rules actions to send data to Kinesis Data Firehose and consume with AWS Lambda 
* Define an ioT rules actions to send data to Kinesis Data Streams and consume the data with AWS Lambda 
* **Define an IoT rules actions to send data to SQS and consume the LI data with EC2 instances in an Auto Scaling group   (Correct)** 
* Define an loT rules actions to send data to Kinesis Data Streams and consume \-1 the data with KCL 

> **Explanation** 
> 
> **Kinesis Data Streams doesn't work because it doesn't scale as the load increases.**
> 
> Kinesis Data Firehose doesn't work as Lambda cannot be a consumer of KDF. Lambda can only be used for transformations of data going through KDF before being delivered to S3, Redshift, ElasticSearch or Splunk. 
> 
> Here the lack of ordering and the fact the processing may be long, and needs to scale based on the number of messages make SQS a great fit, that will also be more cost efficient 


### **Question 20:**

A produce export company has **multi-dimensional data for all of its shipments, such as the date, price, category, and destination of every shipment.** A data analyst wishes to explore this data, with the primary purpose of looking for trends and outliers in the information. 

Which QuickSight visualization would be best suited for this? 

* Stacked horizontal bar chart 
* **Heat map** 
* Pivot table 
* Scatter plot 

> Explanation 
> 
> You can think of heat maps as pivot tables that highlight outliers and trends using color. 

### **Question 21:**

Your data lake in S3 for user transaction data is stored in CSV format. To save costs, data older than one year is archived to Glacier. You have received a request from your legal team to retrieve any records for a specific user ID going back seven years, and they need it today. What is the most cost-effective way to fulfill their request? 

* Import the Glacier data into Redshift and query it there 
* **Use Glacier Select to run a query against the Glacier data for this user ID, and merge it with the same query run with S3 Select.   (Correct)**
* Use S3 Select to automatically query both S3 and Glacier together 
* Restore 7 years' of data from Glacier to S3, query the S3 data with Athena then delete the restored data. 


> **Explanation** 
> 
> Glacier Select allows you to perform filtering directly against Glacier objects using standard SQL statements. It is the simplest, quickest, and most cost-effective option for querying cold data stored in Glacier. 


### **Question 22:**

An Amazon Elasticsearch domain has been installed within a VPC. 

What are TWO methods which could be employed to securely allow access to Kibana from outside the VPC? 

* **Set up a reverse proxy server between your browser and Amazon Elasticsearch servcer (Correct)**
* Configurean IAM policy to your browser to access Kibana. 
* Create a security group to allow your IP access to the subnet attached to the VPC on port 443
* Use KMS between your browser and Kibana. 
* **Set up an SSH tunnel with port forwarding to allow access on on port 5601. (Correct)**

> **Explanation** 
> 
> **Kibana runs on port 5601 by default, so opening up port 443 won't help**. IAM doesn't know about your browser, and KMS does not integrate with Kibana. 

### **Question 23:**

You need to add more nodes to your **Redshift cluster and change the node type in the process. Which process allows you to do this while minimizing downtime**? 

* Short Query Acceleration 
* Elastic resize 
* **Classic resize with snapshot / restore / resize （Correct)**
* WLM 

> **Explanation** 
> 
> While it is possible to change node types with elastic resize, the snapshot / restore / resize approach with classic resize minimizes the downtime involved. Elastic resize only holds connections open if you only change the number of nodes, not the node type. 


**Question 24:** 

What are THREE ways in which **EMR optionally integrates HBase with S3**? 

* **Storage of HBase StoreFiles and metadata on S3  （Correct)**
* **HBase read-replicas on S3 （Correct)**
* Automatic backup from HDFS-based StoreFiles to 
* AWS Glue integration to infer schemas of S3 data 
* **Snapshots of HBase data to S3 （Correct)**

> **Explanation** 
> 
> EMR allows you use S3 instead of HDFS for HBase's data via EMRFS. 
> 
> Although you can export snapshots to S3, 
> 
> HBase itself does not automate this for you. 

### **Question 25:**

**New data arrives in S3 on an irregular schedule that you wish to import into an Amazon Elasticsearch cluster as it is received.** The raw data in S3 requires some custom parsing before it is loaded into Elasticsearch. 

Which solution minimizes ongoing maintenance and maximizes scalability? 

* Use AWS Glue to connect Elasticsearch directly to your S3 bucket 
* Use Spark Streaming on an EMR cluster with reserved instances to monitor the S3 bucket and redirect the data to Elasticsearch 
* Use Kinesis Firehose to pump data from S3 directly into Elasticsearch 
* **Use a Lambda function to respond to event triggers from S3, and stream data from S3 into Elasticsearch as it is received  （Correct)**

> **Explanation** 
> 
> **Glue does not integrate with Elasticsearch**, ruling out "Use AWS Glue to connect Elasticsearch directly to your S3 bucket". 
> 
> **EMR clusters require manual scaling as your needs evolve**, which involves ongoing maintenance we could avoid - so "Use Spark Streaming on an EMR cluster with reserved instances to monitor the S3 bucket and redirect the data to Elasticsearch" is also a poor choice. 
> 
> While Firehose can sit between S3 and Elasticsearch, the requirement to perform custom parsing means a Lambda function would be useful - leading us to "Use a Lambda function to **respond to event triggers from S3, and stream data from S3 into Elasticsearch as it is received" **


### **Question 26:**

A real estate company wishes to display interactive charts on their website summarizing their prior month's sales activity. 

Which TWO solutions would provide this capability in a scalable and inexpensive manner? 


* Use Tableau to visualize the data on the web, backed by an Amazon Aurora RDS database. 
* **Publish data in csv format to Amazon Cloudtront via S3, and use Highcharts to visualize the data on the web. （Correct)**
* **Publish data in csv format to Amazon Cloudfront via S3, and use d3.js to visualize the data on the web. （Correct)**
* Embed Amazon Quicksight into the website, querying an underlying Redshift data warehouse. 
* Embed a Jupyter Notebook hosted on EMR into the website. 

> **Explanation** 
> 
> Both d3 and Highcharts are Javascript libraries intended for interactive charts and graphs on websites. Quicksight and Tableau are data analysis tools not intended for public deployment. 


### **Question 27**

Your company has data from a variety of sources, including Microsoft Excel spreadsheets stored in S3, log data stored in a S3 data lake, and structured data stored in Redshift. 

Which is the simplest solution for providing interactive dashboards that span this data? 

* Create an Excel macro to dump the Excel data to csv files stored in S3, then \-1 use Amazon Quicksight to visualize it and the other data sources together. 
* Create Excel macros to import the log and Redshift data into Excel, and \-1 visualize it all within Excel. 
* **Use Amazon Quicksight directly on top of the Excel, S3, and Redshift data. 
(Correct)** 
Write Python code in a Jupyter Notebook on an EMR cluster that processes LI the data and generates graphs. 

> **Explanation** 
> 
> The key to this question is remembering that **Quicksight can actually consume Excel spreadsheets directly. Knowing that, "Use Amazon Quicksight directly on top of the Excel, S3, and Redshift data." is clearly the simplest approach**. 

### **Question 28:**

You are dealing with PII datasets and **would like to leverage Kinesis Data Streams for your pub-sub solution**. **Regulators imposed the constraint that the data must be encrypted end-to-end using an internal key management system**. What do you recommend? 

* **Implement a custom encryption code in the Kinesis Producer LI Library (KPL) (Correct)**
* Use the Kinesis Client Library (KCL) to encrypt the data 
* Encrypt the data with the MD5 algorithm before pushing it to Kinesis 
* Enable KMS encryption at rest for Kinesis and transfer the data over HTTPS to get in-flight encryption 

> **Explanation** 
> 
> We cannot use KMS as we cannot leverage an internal key management system. MD5 is not an encryption algorithm and encryption must happen at the producer level (KPL), while decryption will happen at the consumption level (KCL). 




### **Question 29**

You are an online retailer and your website is a storefront for millions of products. You have recently run a big sale on one specific electronic and y**ou have encountered Provisioned Throughput Exceptions. You would like to ensure you can properly survive an upcoming sale that will be three times as big**. What do you recommend? 

* **Enable DynamoDB DAX** 
* Triple the provisioned RCU 
* Triple the provisioned WCU 
* Enable DynamoDB Streams 

> **Explanation** 
> 
> Here we are in a hot partition situation where one item is constantly being requested. Adding RCU will be costly and won't be effective as even though we have tripled the table capacity, the one partition will still experience throughput exceptions. Enabling DynamoDB Streams will not help, **but a DAX cluster will provide caching for hot items and will definitely help in this situation**. 


### **Question 30:**

You are collecting data from various IoT thermostat and would like to have the data in S3 to ensure you can perform analytics on it using Hive running on EMR. The data scientists will use Hive to query the data based on a date range and will 
need to delete the data in S3 regularly if it becomes out of date to save cost. 
What do you recommend for the storage strategy in S3? 


* `<device-id>/<YYYY>/<MM>/<DD> `
* All the data at the root of your S3 bucket 
* **`<YYYY>/<MM>/<DD>/<device-id>/ `  (Correct)**
* `<DD>/<MM>/<YYYY>/<device-id>/`

> **Explanation** 
> 
> As all the data will often get queried and deleted based on a date range, **it's much better to use a date as the root key for your S3 objects**. 
> 
> Starting with the year is better as it will allow you to query based on years efficiently. 


### **Question 31**

You are processing data using a long running EMR cluster and you like to ensure that you can recover data in case an entire availability zone goes down, **as well as process the data locally for the various Hive jobs you plan on running**. What do you recommend to do this at a minimal cost? 

* Store the data in S3 and directlyvperform Hive jobs against it 
* **Store the data in S3 and keep a warm copy in HDFS (Correct)** 
* Store the data in HDFS and mirror it to another EMR cluster in another region 
* Enable regular EBS backups 

> **Explanation** 
> 
> EBS backups will be expensive and very painful to deal with as the dataset will be distributed over many different snapshots due to HDFS block replication mechanisms. 
> 
> Storing all the data in S3 and none in HDFS will incur some extra costs as the data is constantly read and written back to S3. 
> 
> **It's better to keep a local copy on HDFS. Finally, maintaining an entirely new EMR cluster for disaster recovery is too expensive**. 


### **Question 32**

You are creating an EMR cluster that will process the data in several MapReduce steps. Currently you are working against the data in S3 using EMRFS, but the network costs are extremely high as the processes write back temporary data to S3 before reading it. You are tasked with optimizing the process and bringing the 
cost down, what should you do? 

* **Add a preliminary step that will use a S3DistCp command**
* Use I3 type of instances 
* Enable EMRFS local caching feature 
* Enable LUKS encryption 


> **Explanation** Here, using an **S3DistCp command is the right thing to do to copy data from S3 into HDFS and then make sure the data is processed locally by the EMR cluster MapReduce job**. Upon completion, you will use S3DistCp again to push back the final result data to S3. LUKS encryption will not help, EMRFS does not have a local caching feature, and changing the EC2 instance types won't help 

### **Question 33:** 

What security mechanisms are supported by tMFC' (Select three) 

* **KMS encryption (Correct)** 
* **LUKS encryption (Correct)** 
* **SSE-KMS (Correct)** 
* External HSM encryption 
* Transparent Data Encryption (TDE) 
* SSE-C 

> **Explanation** https://aws.amazon.com/blogs/big-data/best-practices-for-securing-amazon-emr/ 


### **Question 34:** 

An application processes sensor data in real-time by publishing it to Kinesis Data Streams, which in turn sends data to an AWS Lambda function that processes it and feeds it to DynamoDB. During peak usage periods, it's been observed that some data is lost. **You've determined that you have sufficient capacity allocated for Kinesis shards and DynamoDB reads and writes**. 

What might be TWO possible solutions to the problem? 

* Allocate more Lambda nodes 
* Enable replication in Lambda 
* Provision more Kinesis shards 
* **Process data in smaller batches to avoid hitting Lambda's timeout (Correct)** 
* **Increase your Lambda function's timeout value (Correct)** 


> **Explanation** 
> 
> Lambda is serverless, and you don't need to concern yourself with how many nodes it might be using under the hood, or how it automatically handles replication and redundancy. However, lambda functions do have a timeout associated with them, and if the processing you're doing takes longer than this, events will be rejected. 

### **Question 35:** 

A financial services company wishes to back up its encrypted data warehouse in Amazon Redshift daily to a different region. 

What is the simplest solution that preserves encryption in transit and at rest? 


* Configure a second Redshift cluster in another region, and use a daily COPY  command triggered by Lambda to transfer the encrypted data to the other cluster. 
* Move the data into S3 and use Amazon Redshift from multiple regions to query it. 
* **Configure Redshift to automatically copy snapshots to another region, using an AWS KMS customer master key in the destination region.  (Correct)**
* Configure Redshift to replicate its data to a standby cluster in another region. 

> **Explanation** 
> 
> Note that we said "daily," which means we don't need real-time replication. Snapshots will do just fine. 
> 
> "Move the data into S3 and use Amazon Redshift from multiple regions to query it." is a little bit misleading, as it doesn't matter where you run Redshift itself from if the data is stored elsewhere - but moving the data isn't exactly a simple solution. 

**Question 36**

You would like to design an application that will be able to sustain storing 100s of TB of data in a database that will **get low latency on reads and won't require you to manage scaling**. What do you recommend? 

* Redshift 
* Aurora 
* **DynamoDB   (Correct)**
* ElastiCache 

> **Explanation** 
> 
> **Redshift cannot be used for low latency reads, Aurora will not scale past 64 TB and ElastiCache most likely won't scale and require you to manage scaling anyway**. 
> 
> DynamoDB complies with the requirements and has built-in support for auto scaling. 


### **Question 37:**

A MapReduce job on an EMR cluster needs to process data that is currently stored in very large, compressed files in HDFS, which limits the cluster's ability to distribute its processing.
 
Which TWO solutions would best help the MapRedue job to operate more efficiently? 

* **Uncompress the data and split it into 64MB chunks (CorrecT)** 
* Compress the file with Snappy 
* **Convert the file to AVRO format (Correct)** 
* Compress the file with GZIP 
* Uncompress the data and split it into 64K chunks 

> **Explanation** 
> 
> **AVRO is a format that can easily be split and distributed by MapReduce as needed**. Alternately, the data could be split manually into different files - but ideally you'd want these files to be close to the default HDFS chunk size of 64MB in order to make the best use of HDFS. 


### **Question 38:** 

You have an S3 bucket that your entire organization can read. For security reasons you would like the data sits encrypted there and you would like to define a strategy in which users can only read the data which they are allowed to decrypt, which may be a different partial set of objects within the bucket for each 
user. How can  “nn achieve that? 

* **Use SSE-KMS to encrypt the files (Correct)**
* Change the bucket policy 
* Use SSE-S3 to encrypt the files 
* Use identity federation 


> **Explanation** 
> 
> Here, the key is that users should be able to decrypt different files based on their rights. 
> 
> **Bucket policies do not scale for that matter if you have a lot of users and diverse data directories**. 
> 
> SSE-S3 uses only one encryption key and does not enable granular permissions. Identity federation would not help either to solve that problem, as it does not define an authorization model. 
> 
> SSE-KMS will allow you to use different KMS keys to encrypt the objects, and then you can grant users access to specific sets of KMS keys to give them access to the objects in S3 they should be able to decrypt. 



### **Question 39**

You are working for an e-commerce website and that website uses an on-premise PostgreSQL database as its main OLTP engine. You would like to perform analytical queries on it, but the Solutions Architect recommended not doing it off of the main database. What do you recommend? 

* Use DMS to replicate the database to RDS 
* Create an on-premise PostgreSQL Read Replica 
* Create an RDS Read Replica 
* Create an Aurora Read Replica 

> **Explanation** Read Replicas cannot be instantiated from an on-premise database. Here using a solution like DMS (Database Migration Service) is the right way to replicate the database state. 


### **Question 40**

A manager wishes to make a case for hiring more people in her department, by showing that the number oming tasks for her department have grown at a faster rate than other departments over the past year. 

Which type of graph in Amazon Quicksight would be best suited to illustrate this 

* Heat map 
* A sequence of slides in a QuickSight Story 
* **Area line chart （Correct)** 
* Stacked vertical bar chart 


> **Explanation** 
> 
> When you're **looking for trends over time, line charts** are usually the right choice. 



### **Question 41:**  

You wish to analyze an S3 data lake using standard SQL. Which solution results in the least amount of ongoing administration from you, as your data grows? 

* Apache Spark on EMR 
* **Amazon Athena （Correct)** 
* Amazon Redshift Spectrum 
* Amazon RDS 


> **Explanation** 
> 
> Of the above choices, only Amazon Athena is a "serverless" solution that does not require you to provision capacity as your data and usage grows. 


### **Question 42: **

As part of your application development, you would like your users to be able to get Row Level Security. The application is to be deployed on web servers and the users of the application should be able to use their `amazon.com` accounts. What do you recommend for the database and security? 

* Enable Web Identity federation. Use RDS and reference `${www.amazon.com:user_id}` in the attached IAM policy 
* Enable Web Identity federation. Use DynamoDB and reference `${aws:username}` in the attached IAM policy 
* Enable Web Identity federation. Use DynamoDB and reference `${www.amazon.com:user_id}` in the attached IAM policy 
* Enable Web Identity federation. Use RDS and reference `${aws:username}` in the attached IAM policy 

> **Explanation** 
> 
> **RDS does not allow authorization through IAM policies**, so we have to rule out RDS as a database technology for our purpose. 
> 
> DynamoDB is the technology of choice. **As we're using Web Identity Federation with amazon.com, our IAM policy should use the `${www.amazon.com:user_id}` policy variable** 



### **Question 43**

Your financial organization has hundreds of Terabytes of data stored within its on premise data centers, and data is being produced at the rate of Gigabytes per second, and could be consumed within 3 days. As part of their AWS cloud migration, what solution do you recommend for them? 

* **Transfer your historical data using Snowball and use Kinesis Data Streams for ongoing data collection.  (Correct) **

* Install Direct Connect between your data center and AWS and transfer all the data over a 10Gbps line. Use Kinesis Data Firehose for ongoing data collection. 
* Transfer your historical data using Snowball and use Kinesis Data Firehose for ongoing data collection. 
* Install Direct Connect between your data center and AWS and transfer all the Li data over a 10Gbps line. Use Kinesis Data Streams for ongoing data collection. 


> **Explanation** As your organization has **hundreds of Terabytes of data, it is going to be much quicker and much more efficient to use Snowball to transport that data to AWS**. 
> 
> As the data streams must be stored for at least 3 days, you must use Kinesis Data Streams which has a configurable data retention of between 1 and 7 days. 


### **Question 44:**

You have programmed a Lambda function that will be automating the creation of an EMR cluster, which in turn should perform some transformations in S3 through EMRFS. Your Lambda function will be triggered by Cloud Watch Events. How can you ensure your Lambda function can properly perform its actions? 

* Deploy in a VPC
* Use a Lambda policy  
* **Attach an IAM role   (Correct)**
* Attach an IAM user 

> **Explanation** As the Lambda function will be performing API calls on our infrastructure, it needs to have an IAM role attached. Deploying it in a VPC won't help, and we can't create users for Lambda functions. 


as possible and without impacting the current read an 

### **Question 45:** 

As part of an effort to limit cost and maintain under control the size of your DynamoDB table, your AWS account manager would like to ensure old data is deleted in DynamoDB after 1 month. How can you do so with as little maintenance d write operations? 

* **Enable DynamoDB TTL and add a TTL column (Correct)**
* Create a Lambda function that gets triggered on a daily basis 
* Create a lifecycle rule to delete your items after 30 days 
* Scan your table from EMR and issue a delete statement afterwards 

> Explanation Lifecycle rules do not exist on DynamoDB, and a Lambda function would require maintenance and add load on the WCU as you delete items. So will an EMR scan. The TTL will automatically expire old items and will not affect your usage of WCU and RCU upon item deletion. 



### **Question 46:**

Which are the two technologies that support VPC Endpoint Gateway? (select two) 

* **DynamoDB (Correct)** 
* **SQS (Correct)** 
* SNS 
* CloudFormation 


> **Explanation** DynamoDB & S3 are the only technologies that have VPC Endpoint Gateways, the rest are VPC Endpoint Interfaces. 


### **Question 47:**

A data scientist wishes to develop a machine learning model to predict stock prices using Python in a Jupyter Notebook, and use a cluster on AWS to train and tune this model, and to vend predictions from it at large scale. 

Which system allows you to do this?

* **Amazon SageMaker (Correct)** 
* Apache Zeppelin 
* Amazon Machine Learning 
* Amazon Comprehend 


> **Explanation** 
> 
> SageMaker enables developers and data scientists to build, train, and deploy machine learning models at any scale, using hosted Jupyter notebooks. Zeppelin also uses a hosted Jupyter notebook, but does not integrate with AWS to train and tune models. Amazon Machine Learning does not use notebooks, and Amazon Comprehend is a natural language processing tool. 


### **Question 48**

You are looking to query data storage in DynamoDB from your EMR cluster. Which of the following technology will allow you to do so? 

* **Hive (Correct)** 
* Pig 
* Spark 
* HBase 


> **Explanation** 
> 
> Amongst the four listed above, Hive can have DynamoDB as a source for its queries. 


**Question 49:** 

A produce export company has multi-dimensional data for all of its shipments, such as the date, price, category, and destination of every shipment. A data analyst wishes to interactively explore this data, applying statistical functions to different rows and columns and sorting them in different ways. 

Which QuickSight visualization would be best suited for this? 

* Stacked horizontal bar chart 
* Heat map 
* **Pivot table** 
* Scatter plot 


> **Explanation** 
> 
> **Interactive exploration of multi-dimensional data usually calls for a pivot table**, as long as you're not looking to quickly identify outliers at the same time. 


### **Question 50**

You are storing gaming data for your game that is becoming increasingly popular. An average game data will contain 80KB of data and as your games are quick. **You expect about 400 games to be written per second to your database. Additionally, a lot of people would like to retrieve this game data and you expect about 1800 eventually consistent reads per second**. How should you provision your DynamoDB table? 

* 3200 WCU & 36000 RCU 
* **32000 WCU & 18000 RCU (Correct)** 
* 32000 WCU & 144000 RCU 
* 32000 WCU & 36000 RCU 

> **Explanation** 
> 
> `1 WCU = 1 KB/s` so we need 
> 
> `80KB * 400/s = 32000 WCU`. `1 RCU = 2` eventually consistent reads per second of 4 KB so we need `1800 * 80 / 8 = 18000 RCU`. 


### **Question 51**

Which tool on Amazon Elastic MapReduce allows you to monitor your cluster's performance as a whole, and at individual nodes? 

* Presto 
* **Ganglia (Correct）** 
* Hue
* Ambbari

> **Explanation** 
> 
> **Ganglia is the operational dashboard provided with EMR. Hue and Ambari are graphical front-ends for interacting with a cluster, but only Hue is provided with EMR.** 
> 
> Presto is used for querying multiple data stores at once. 


### **Question 52**

As an e-cornmerce retailer, you would like to onboard **clickstream** data onto **Kinesis from your web servers Java applications**. **You want to ensure that a retry mechanism is in place, as well as good batching capability and asynchronous mode.** You also want to collect server logs with the same constraints. What do you recommend? 

* Use the Klnems Agent to se. the ell, stream and collect the server logs
* Use the AWS Kinesis SDK for Java in your web servers and use Kness 0 Producer Lama, to collect server logs 
* **Use the Knems Producer Library to send the Clickstream and the Kineis agent to collect the Server Logs (Correct）** 
* Use Kinesis Producer Library to send the ell, stream and collect the server 

> **Explanation** 
> 
> The KPL has the mechanisms in place for retry and batching, as well as asynchronous mode. The Kinesis agent is meant to retrieve server logs with lust configuration files. 


### **Question 53**

You are working for a bank and your company is regularly uploading 100 MB files to Amazon S3 and analyzed by Athena. **It has come to light that recently some of the uploads have been corrupted and made a critical big data job tails**. Your company would like a stronger guarantee that uploads are done successfully and that the files have the some content on premise and on S3. It looks to do so at minimal cost. What do you recommend? 


* Upload a hash header as part of the S3 metadata which will trigger an S3 failure upon server side check for corruption 
* **Use the S3 Etag and compare to the local MD5 hash  (Correct)** 
* Transfer the data over HTTP with gzip compression enabled 
* Download the data from S3 after uploading it a. compare the SHA-1 signature 

> **Explanation** 
> 
> Here the S3 tag will compute the MD5 hash of the file on the server and this can be used to compare it to the local MD5 hash of the file that has been uploaded. 
> 
> Downloading data back from S3 might work, but will be way too costly. There's no feature to upload a hash header to S3 and transferring the data on HTTP will not help, and will decrease security. 


### **Question 54**

Your esports application hosted on AWS need to process game results **immediately in real time and later perform analytics on the same game results in the order they came at the end of business hours**. Which of the AWS service will be the best fit for your needs? 

* SQS FIFO Queues 
* DynamoDB
* **Kinesis Data Streams (Correct)** 
* SQS Standard Queues 

> **Explanation** 
> 
> Here **Kinesis is the best fit as the data can be replayed in the same order.** 
> 
> **SQS does not allow data replays, and DynamoOB would allow to replay some data, but it'd be different to get some ordering constraints working as well as well as enable real time use cases**. 

### **Question 55**

You are required to maintain a real-time replica of your **Amazon Redshift data warehouse across multiple availability zones**. 

What is one approach toward accomplishing this? 

* Snapshot your Redshift to Amazon S3, and copy it to a different availability zone periodically from a Lambda function 
* Enable the trulti-AZ option when creating your Redsrytt cluster 
* **Spin up separate redshibt clusters in multiple availability zones, using Amazon Kinesis to simultaneously write data into each cluster. Use Route 53 to direct your analytics tools to the nearest cluster when querying your data.    (Correct)**
* Snapshot your Redshift data to Amazon S3, where it may be restored from any availability zone, 

> **Explanation** 
> 
> Redshift does not come with multi-AZ redundancy, so this is something you must build yourself as described in **"Spin up separate redshift clusters in multiple availability zones, using Amazon Kinesis to simultaneously write data into each cluster**. 
> 
> **Use Route 53 to direct your analytics tools to the nearest cluster when querying your date**. 
> 
> **As S3 is mutli-AZ, snapshotting your data to S3, which Redshift does do automatically, does provide you with some protection - but it does not satisfy the real-bore replication requirement stated in the question**. 


### **Question 56**

Your daily Spark jobs runs against files created by a Kinesis Firehose pipeline in S3. **Due to a low throughput, you observe that each of the many files created by Kinesis Firehose is about 100KB**. You would like to optimise your Spark job as best as possible to query the data efficiently. What do you recommend? 

* Use multl-part download with Spark. 
* Compress the files using GZIP 
* **Consolidate files on a daily basis usng DataPipeline  (Correct)**
* Increase the batch flush time in Mnesis Data Firehose to 1 hour 

> Explanation 
> 
> Multi part download is not a Spark feature, which does not deal well with many small files. 
> 
> GZIP will not solve the problems, the files will still be small and you will have many of them. Kinesis Data Firehose does not haves flush time greater than 5 minutes, which will still create many small files. Bottom line, you should use a DataPipeline job to consolidate the files on a daily basis into a larger file. 


### **Question 57**

You have an ETL process that collects data from different sources and 3rd party providers and **would be to ensure that data is loaded into Redshift once all the parts from all the providers related to one specific jobs have been gathered,** which is the process that can happen over the course of one hour to one day. What the least costly way of doing that? 

* Use the multi part upload feature of S3 to collect data from different sources 
* **Create an AWS Lambda that responds to S3 upload events and will check if all the parts are there before uploading to Redshift  (Correct)**
* Create a Kinesis Data Firehose pipeline and program a Python condition that will trigger a buffer flush upon receiving all the necessary parts 
* Load data in Redshif regularly using a Lambda cron job into a temporary table and use Redshift database triggers to assemble the final clata when all the parts are ready. 


> **Explanation** 
> 
> Loading the data in Redshift will be costly and inefficient and Redshift does not support database triggers. 
> 
> Multi Part is not helpful for data coming from various sources. Kinesis Firehose does not have a Python condition for buffer flush (only time and size). 
> 
> **Here a Lambda function that reacts to events happening in $3 is the right answer**. 


### **Question 58**

You work for a gaming company and each game's data is stored in DynamoDB tables. **In order to provide a game search functionality to your users, you need to move that data over to ElasticSearch**. How can you achieve it efficiently and as close to real time as possible? 

* Enable DynamoDB Streams and connect it with Kinesis Data Firehose
* Create a DataPipeline job scheduled on ab hourly basis
* **Enable DynamoDB Streams and write a Lambda function (Correct)**
* Use DynamoDB Global Rephcation and select ElastmSearch Service as your target

> **Explanation** 
> 
> **DynamoDB Streams do not have direct integration with Firehose**,
> 
> DataPipeline will not have the data fast enough into ElasticSearch, and DynamoDB Global Tables do not integrate with ElasticSearch. 
> 
> **Here we need to write a Lambda function that is triggered from a DynamoDB Stream** 



### **Question 59**

You have created a system that recommends items similar to other items on an e-commerce website, by training a recommender system **using Mahout on an EMR cluster**. 

Which would be a performant means to vend the resulting table of similar items for any given item to the website at high transaction rates?
 
* **Publish the data into HBase (Correct)** 
* Load the data Into a Redshdt cluster and query It from the website
* Expose the data via Hive and JDBC 
* Load data mto Amazon Aurora / HOS and query It from website
 
> **Explanation** 
> 
> This is an OLTP use case for which a "NoSQL" database is a good fit HBase is the only option presented designed tor OLTP and not (KAP, plus it has the advantage of already being present in EMR. 
> 
> DynamoDB would also be an appropriate technology to use. 


### **Question 60**

You wish to use Amazon Redshitt Spectrum to analyze data in an Amazon S3 bucket that is in a different account than Redshift Spectrum. 

How would you authorize access between Spectrum and S3 across accounts? 

* **Add a ploicy to the S3 bucket allowing S3 GET and LIST operations for an IAM role for Spectrum on the Redshift account (Correct)**
* Add a policy to the S3 bucket allowing S3 GET and LIST operations for the user agent "AWS Redshift/Spectrum"
* Create an IAM role allowing access for COPY operations on S3 
* Create a VPC endpoint to S3 accessible by your Redshift Spectrum


> **Explanation** 
> 
> Only "Add a policy to the S3 bucket allowing S3 GET and LIST operations for an IAM role for Spectrum on the Redshift account" specifically addresses the problem of cross-account access to the S3 bucket. 

### **Question 61**

Your enterprise would like to leverage AWS Redshift to query data. Currently that data is produced at the rate of 5 PB of historical data and another 3 TB per month that you would like to get with less than two days delay, and you are tasked with finding the most efficient data transfer solution into S3. What do you recommend? (select two) 

* Use Snowball to transfer the newly created monthly data 
* Establish Direct Connect transfer the historical data over a 10Gpbs connection 
* **Use Snowball to transfer the historical data (Correct)** 
* **Establish Direct Connect and do a daily upload created monthly data directly into S3  (Correct)**
* Establish Site-to-Site VPN and transfer the historical data over a public 10Gbps connection


> **Explanation** 
> 
> Snowball is the only way to transfer your historical data as it would take a very long time to transfer over the network, even with Direct Conned or Site-to-Site VPN. 
> 
> For ongoing data, it's the equivalent of 300 GB a day, which will take less than an hour to upload each day versus Snowball which will definitely take longer than 2 days to reach AWS. 


### **Question 62**

You need to load several hundred GB of data every day from Amazon 53 into Amazon Redshift, which is stored in a single file. You've found that loading this data is prohibitively slow. 

Which approach would optimize this loading best? 

* Avoid loading the data in the same order as your sort key. 
* Split the data into fres between 1GB and 125GB rafter compressiond and specify GZIP compression from multiple COPY commands run concurrently 
* **Split the data into fres between 1MB and 125MB (after comprssion) and specify GZIP conhoression from a single COPY command (Correcrt)** 
* Split the data into files between 1MB and 125MB (after compressiond and specify GZIP compression from multiple COPY commands run concurrently 


> **Explanation** 
> 
> Multiple concurrent COPY commands might sound like a good idea, but in reality it forces Redshift to perform a slow, serialized load followed by a VACUUM Process, If you want to load data in parallel, it's best to split your data into separate files no more than 1GB apieåce. 
> 
> Compressing the data also helps. Loading data in the same order as your sort key can also speed up the import process, which is the opposite of "Avoid loading the data in the same order as your sort key".


### **Question 63**

Your team has developed a Spark Streaming applications that performs real time transformations on an on-premise Apache KM ka cluster and finally delivers the data in real time to S3. As part of a migration to the cloud and switch to Kinesis as an underlying streaming store, what do you recommend? 

* Produce data using Spark Streaming to Kinesis Data Streams, and read the o data with Spark Streaming frorn Kinesis Data Frehose to write it to S3 
* Produce data using Spark Streaming to Kinesis Data Firehose and deliver the data to S3 using Kinesis Data Firehose. 
* Produce data using Spark Streaming to Kinesis Data Firehose and deliver the data S3 using Spark Streaming reading from Kinesis Data Streams. 
* **Produce data using Spark Streaming to Kinesis Data Streams, and read the data min Spark Streaming from Kinesis Data Streams to write it to S3. 
(Correct)** 

> **Explanation** 
> 
> Here, the key requirement is the real-time constraint Kinesis Data Firehose is near real time" (60 seconds minimum batch size) and thus cannot be used tor delivery to S3 in real time. Finally, Spark Streaming can read and write to Kinesis Data Streams only. 




### **Question 64**

**An application on AWS generates frequent logs on S3**. The operational support team needs to analyze the logs to understand various patterns of the application failures and try to come up with a plan to fix those issues. Which option is cost-effective and requires the LEAST engineering effort? 

* **Create AWS Glue Data Catalogue metadata and analyze logs via Amazon Athena.  (Correct)**
* Download Me log files Korn SS and manually check the failure reasons. 
* Migrate the logs to the Elasticsearch platform and analyze further using Kihana. 
* Create AWS Glue Data Catalogue metadata and spin up an ENID cluster with a Hive metastore pointing to AWS Glue Data Catalogue. Use Spark and Hive to analyze the logs further. 

> **Explanation** 
> 
> **Amazon Athena is meant for analysis of files on S3 after creation of metadata on AWS Glue**. 


### **Question 65**

You need to ETL streaming data from web server logs as it is streamed in, for analysis in Athena. Upon talking to the stakeholders, you've determined that the ETL does not strictly need to happen in real-time, but transforming the data within a minute is desirable. 

What is a viable solution to this requirement? 

* **Perform any initial ETL you can using Amazon Kinesis, store the 0 data in S3, and trigger a Glue ETL job to complete the transformations needed. (Correct)**
*  Perform any initial ETL you can with Kinesis Analytics, and send Me output of 0 Kinesis Analytios directly. a Spark Streaming application to Olathe remaining transformations. 
*  Create an AWS Glue ETL job, and schedule it to it every minute 
*  Publish your data into DynamoDB, and use DynamoDB strearns together with AWS Glue to perform the ETL 


> **Explanation** 
> 
> 
> Glue jobs can be scheduled at a minimum of 5 minutes, ruling out "Create an AWS Glue ETL job, and schedule it to run every minute". 
> 
> Glue does not integrate directly with DynamoDB, ruling out "Publish your data into DynamoDB, and use DynamoDB streams together with AWS Glue to perform the ETL"
> 
> Kinesis Analytics cannot connect directly to Spark Streaming, ruling out "Perform any initial ETL you can with Kinesis Analytics, and send the output of Kinesis Analytics directly to a Spark Streaming application to handle the remaining transformations"
> 
> "Perform any initial ETL you can using Amazon Kinesis, store the data in S3, and trigger a Glue ETL job to complete the transformations needed." is the recommended approach from AWS. An alternative approach would be to use Kinesis Firehose and a Lambda function to transform the data before storing it in S3. 
