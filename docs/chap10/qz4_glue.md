# **Quiz4 AWS Glue**

Check your knowledge on some of the finer points of AWS Glue crawlers, data catalogs, and ETL jobs.

### **Question 1**

You want to load data from a MySQL server installed in an EC2 t2.micro instance to be processed by AWS Glue. What applies the best here?

* Not possible with instance, must use RDS 
* MySQL configuration should have glue support enabled 
* **Instance should be in your VPC** 

> Although we didn't really discuss access controls, you could arrive at this answer through process of elimination. You'll find yourself doing that on the exam a lot. This isn't really a Glue specific question; it's more about how to connect an AWS service such as Glue to EC2.

### **Question 2**

What is the simplest way to make sure the metadata under Glue Data Catalog is always up-to-date and in-sync with the underlying data without your intervention each time?

* **Schedule crawlers to run periodically** 
* Using Glue API 
* Using the AWS console 

> Crawlers may be easily scheduled to run periodically while defining them.

### **Question 3**

Which programming languages can be used to write ETL code for AWS Glue?

* Python and Java 
* **Python and Scala** 
* Python and Node.js 
* Scala and C# 

> Glue ETL runs on Apache Spark under the hood, and these happen to be the primary languages used for Spark development.

### **Question 4**

Can you run existing ETL jobs with AWS Glue?

* Yes

> You can run your existing Scala or Python code on AWS Glue. **Simply upload the code to Amazon S3 and create one or more jobs that use that code. You can reuse the same code across multiple jobs by pointing them to the same code location on Amazon S3.**

### **Question 5**

How can you be notified of the execution of AWS Glue jobs?


* **Using Cloudwatch + SNS** 
* Using Cloudwatch + SES 
* Using Glue events + SES 

> AWS Glue outputs its progress into CloudWatch, which in turn may be integrated with the Simple Notification Service.

