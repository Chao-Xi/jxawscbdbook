# **Quiz3 AWS Lambda**

### **Question 1**

You are going to be working with objects arriving in S3. Once they arrive you want to use AWS Lambda as a part of an AWS Data Pipeline to process and transform the data. How can you easily configure Lambda to know the data has arrived in a bucket?

* Run a cron job to check for new objects arriving in S3 
* **Configure S3 bucket notifications to lambda** 
* Configure S3 versioning to include writing logs to Lambda Use
* Cloudwatch logs and have Cloudwatch events trigger Lambda. 

> Lambda functions are generally invoked by some sort of trigger. S3 has the ability to trigger a Lambda function whenever a new object appears in a bucket.


### **Question 2**

You are going to analyze the data coming in an Amazon Kinesis stream. You are going to use Lambda to process these records. What is a prerequisite when it comes to defining Lambda to access Kinesis stream records ?

* **The Kinesis stream should be in the same account** 

> Lambda must be in the same account as the service triggering it, in addition to having an IAM policy granting it access.

* The stream should not be older than 3 hours 
* The Kinesis stream should have its policy document to allow for AWS Lambda 

> It's actually Lambda that needs an IAM policy allowing Kinesis access, not the other way around.

* None of these 

### **Question 3**

How can you make sure your Lambda functions have access to the other resources you are using in your big data architecture like S3, Redshift, etc.?

* Using a lifecycle policy for lambda 
* Using proper IAM users 
* **Using proper IAM roles** 
* Using Cognito pools. 


> IAM roles define the access a Lambda function has to the services it communicates with.

### **Question 4**

You are creating a Lambda - **Kinesis stream environment in which Lambda is to check for the records in the stream and do some processing in its Lambda function**. How does Lambda know there has been changes / updates to the Kinesis stream ?

* Kinesis streams has options to configure cron jobs to invoke Lambda 
* Cloudwatch logs notify Lambda 
* Kinesis streams notify lambda 

>  Conceptually this might be how you think of a Lambda trigger, but it's not how it actually works under the hood.

* **Lambda polls Kinesis streams** 

> Although you think of a trigger as "pushing" events, Lambda actually polls your Kinesis streams for new activity.

### **Question 5**

When using an Amazon Redshift database loader, how does Lambda keep track of files arriving in S3 to be processed and sent to Redshift ?

* **In a DynamoDB table**
* In Lambda memory 
* In Lambda parameters 
* In Redshift cluster memory 