# **L4 Amazon Elasticsearch Service Exercise**

## **1、Near-real-time log analysis**

![Alt Image Text](../images/24_1.png "body image") 

### **1-1 Cenerate Fake Log**

```
$ pwd
/home/ec2-user

$ wget http://media.sundog-soft.com/AWSBigData/httpd.zip
--2020-02-12 00:27:39--  http://media.sundog-soft.com/AWSBigData/httpd.zip
Resolving media.sundog-soft.com (media.sundog-soft.com)... 52.217.38.124
Connecting to media.sundog-soft.com (media.sundog-soft.com)|52.217.38.124|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 39403376 (38M) [application/octet-stream]
Saving to: 'httpd.zip'

httpd.zip                      100%[===================================================>]  37.58M  48.3MB/s    in 0.8s    

2020-02-12 00:27:40 (48.3 MB/s) - 'httpd.zip' saved [39403376/39403376]


$ unzip httpd.zip
$ sudo mv httpd /var/log/httpd
```

## **2、Create Amazon ES** 

*  **Create a new domain**
*  Deployment type: **Development and testing**
*  Elasticsearch version: **6.8**
*  Elasticsearch domain name: **cadabra**

![Alt Image Text](../images/24_2.png "body image") 

* Network configuration: **Public access** (Not recommended, only for exercise)
* **Uncheck**: **Enable fine-grained access control**
* Access policy: 
	* Custom Access Policy
	* IAM ARN
	* **arn:aws:iam::...:user/jacob.xi**
	* allow

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"  
      },
      "Action": "es:*",
      "Resource": "arn:aws:es:us-east-1:371089343861:domain/cadabra/*"
    }
  ]
}
```



## 3、Create firehose delivery stream and Lambda function 

* New delivery stream: **Weblogs**

### **3-1 Lambda function to transform source**

* Transform source records with AWS Lambda: **Enabled**
* **Create New**: **Apache Log to JSON**

![Alt Image Text](../images/24_3.png "body image") 

![Alt Image Text](../images/24_4.png "body image") 

* FunctionNameParameter: **LogTransform**
* TableNameParameter: **LogTransform**

![Alt Image Text](../images/24_5.png "body image") 

* **Change timeout to: 1 minute**

![Alt Image Text](../images/24_6.png "body image") 


### **3-2 Add Amazon ElasticSearch Service**

![Alt Image Text](../images/24_7.png "body image") 

* Domain: **cadabra**
* index: **weblogs**
* index rotation: **1day**
* Type: **weblogs**

![Alt Image Text](../images/24_8.png "body image") 

### **3-3 Add S3 backup**

* S3: **kin-orderlogs**
* prefix: **es/**

![Alt Image Text](../images/24_9.png "body image") 

### **3-4 ElasticSearch Service buffer condition**

* buffer interval: **300s**
* buffer size: **5MB**

![Alt Image Text](../images/24_10.png "body image") 


### **3-5 Create new default firehose IAM role: `firehose_delivery_role`**

![Alt Image Text](../images/24_11.png "body image") 

### **3-6 Add `aws-kinesis-agent` new config**

```
$ ssh -i ...
$ sudo vi /etc/aws-kinesis/agent.json

{
  "cloudwatch.emitMetrics": true,
  "kinesis.endpoint": "kinesis.us-east-1.amazonaws.com",
  "firehose.endpoint": "firehose.us-east-1.amazonaws.com",

 // "awsAccessKeyId": "",
 // "awsAccessAccessKey": ""

  "flows": [
    {
      "filePattern": "/var/log/httpd/ssl_access*",
      "deliveryStream": "Weblogs",
      "initialPosition": "START_OF_FILE"    
    }
  ]
}


$ sudo service aws-kinesis-agent restart
aws-kinesis-agent startup                                  [  OK  ]
```

![Alt Image Text](../images/24_13.png "body image") 


### **3-7 Check Amazon ES indices**

![Alt Image Text](../images/24_14.png "body image") 


## **4、Kibana**

![Alt Image Text](../images/24_15.png "body image") 

![Alt Image Text](../images/24_16.png "body image") 

### **4-1 Add new index**

* Index pattern: **`weblogs*`**
* Time Filter field name： `@timestamp`

![Alt Image Text](../images/24_17.png "body image") 

![Alt Image Text](../images/24_18.png "body image") 

### **4-2 Add visualize**

![Alt Image Text](../images/24_19.png "body image") 
