# **L2 AWS Services Security Deep Dive**

## **1、Security Kinesis** 

### **1-1 Kinesis Data Streams** 

* SSL endpoints using the HTTPS protocol to do encryption in flight 
* **AWS KMS provides server-side encryption [Encryption at rest]** 
* For **client side-encryption**, you must use your **own encryption libraries** 
	*  No support from AWS
	*  Use the KPL the producer library and own encryption libraries
* Supported Interface VPC Endpoints / Private Link — access privately
* KCL — **must get read / write access to DynamoDB table** 

### **1-2 Kinesis Data Firehose:** 

* **Attach IAM roles so it can deliver to S3 / ES / Redshift / Splunk** 
* **Can encrypt the delivery stream with KMS [Server side encryption**] 
* Supported Interface **VPC Endpoints / Private Link access** privately 

### **1-3 Kinesis Data Analyics** 

* Attach IAM role so it can read from Kinesis Data Streams and reference sources and write to an output destination (example Kinesis Data Firehose) 


## **2、Security - SQS** 

* **Encryption in flight using the HTTPS endpoint** 
* Server Side Encryption using KMS 
* IAM policy must allow usage of SQS
* SQS queue access policy

 
* **Client-side encryption must be implemented manually** 
* VPC Endpoint is provided through an Interface 


## **3、Security —AWS ioT**

### **3-1 AWS ioT policies**: 

* **Attached to X.509 certificates or Cognito Identities** 
* Able to revoke any device at any time  
* IoT Policies are JSON documents like IAM policy 
* Can be attached to groups instead of individual Things. 

### **3-2 IAM Policies**: 

* Attached to users, group or roles 
* Used for controlling IoT AWS APIs 

**Attach roles to Rules Engine so they can perform their actions **

## **4、Security —Amazon S3** 

* IAM policies 
* S3 bucket policies 
* Access Control Lists (ACLs) 
* **Encryption in flight using HTTPS** 
* Encryption at rest 
	* S**erver-side encryption: SSE-S3, SSE-KMS, SSE-C** 
	* Client-side encryption — such as Amazon S3 Encryption Client 
* Versioning + MFA Delete 
* **CORS for protecting website**s
	*  Only a few websites get access to S3 Buckets 
* VPC Endpoint is provided through a Gateway 
* Glacier vault lock policies to prevent deletes (WORM) 
	*  **Write once read many**

## **5、Security DynamoDB** 

* **Data is encrypted in transit using TLS (HTTPS)** 
* **DynamoDB can be encrypted at rest** 
	* KMS encryption for base tables and secondary indexes
	* Only for new tables 
	* **To migrate un-encrypted table, create new table and copy the data** 
	* Encryption cannot be disabled once enabled 
* **Access to tables / API / DAX using IAM** 
* DynamoDB Streams do not support encryption 
* **VPC Endpoint is provided through a Gateway** 


## **6、Security RDS** 

* VPC provides network isolation 
* Security Groups control network access to DB Instances 
* **KMS provides encryption at rest** 
* **SSL provides encryption in-flight** 
* IAM policies provide protection for the RDS API 
* IAM authentication is supported by **PostgreSQL and MySQL** 
* Must manage user permissions within the database itself **unlike  DynamoDB**
* MSSQL Server and Oracle support TDE (**Transparent Data Encryption**)
	*  Enabled on top of KMS and to provide more encryption	 

## **7、Security Aurora** 

* (very similar to RDS)
* **VPC provides network isolation** 
* Security Groups control network access to DB Instances 
* **KMS provides encryption at rest** 
* **SSL provides encryption in-flight** 
* IAM authentication is supported by PostgreSQL and MySQL
* Must manage user permissions within the database itself 

## **8、Security Lambda** 

* **IAM roles attached to each Lambda function** 
* Sources 
* Targets 
* **KMS encryption for secrets** 
* SSM parameter store for configurations 
* CloudWatch Logs 
* Deploy in VPC to access private resources 

## **9、Security Glue** 

* IAM policies for the Glue service
* Configure Glue to only access JDBC through SSL
* **Data Catalog: Encrypted by KMS** 
* Connection passwords: **Encrypted by KMS** 
* **Data written by AWS Glue — Security Configurations:** 
	* S3 encryption mode: SSE-S3 or SSE-KMS 
	* CloudWatch encryption mode
	* job bookmark encryption mode 



## **10、Security - EMR** 

* **Using Amazon EC2 key pair for SSH credentials** 
* Attach IAM roles to EC2 instances for: 
	* proper S3 access 
	* for EMRFS requests to S3 
	* DynamoDB scans through Hive 
* EC2 Security Groups 
	* One for master node 
	* Another one for cluster node (core node or task node) 
* Encrypts data **at-rest** for a Spark or a MapReduce job: 
	* EBS encryption, 
	* Open Source HDFS Encryption, 
	* LUKS + EMRFS for S3 
* In-transit encryption(using SSL certificates): node to node communication, EMRFS,TLS 
* **Data is encrypted before uploading to S3**
	* EMR does not allow you to store unencrypted data into S3 
* Kerberos authentication (provide authentication from Active Directory) 
* Apache Ranger: Centralized Authorization (RBAC — Role Based Access) setup on external EC2 


## **11、Security — ElasticSearch Service** 

* Amazon VPC provides network isolation 
* ElasticSearch policy to manage security further 
* Data security by encrypting data at-rest using KMS
* Encryption in-transit using SSL 

* IAM or Cognito based authentication 
* Amazon Cognito allow end-users to log-in to Kibana through enterprise identity providers **such as Microsoft Active Directory using SAML** 

## **12、Security Redshift** 

* VPC provides network isolation 
* Cluster security groups
*  Encryption in flight using the JDBC driver enabled with SSL 
*  Encryption at rest using KMS or **an HSM device (establish a connection with custom HSM device or hardware security module.)**
*  Supports S3 SSE using default managed key 
*  Use IAM Roles for Redshift 
*  To access other AWS Resources (example S3 or KMS) 
*  Must be referenced in the `COPY` or `UNLOAD` command (alternatively paste access key and secret key creds) 

## **13、Security - Athena** 

* IAM policies to control access to the service 
* Data is in S3: **IAM policies, bucket policies & ACLs** 
* Encryption of data according to S3 standards: SSE-S3, SSE-KMS, CSE-KMS 
* Encryption in transit using TLS between Athena and S3 and JDBC enabled by SSL
* Fine grained access using the AWS Glue Catalog 

## **14、Security - Quicksight** 

### **14-1 Standard edition:** 

* IAM users 
* Email based accounts 

### **14-2 Enterprise edition:** 

* Active Directory 
* Federated Login 
* Supports MFA (Multi Factor Authentication) 
* Encryption at rest and in SPICE 

**Row Level Security to control which users can see which rows** 
