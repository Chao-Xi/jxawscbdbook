# **Quiz5 EMR and the Hadoop Ecosystem**

### **Question 1**

Of the following tools with Amazon EMR, which one is **used for querying multiple data stores at once**?  

* **Presto** 
* Hue
* Ganglia 
* Ambari 

### **Presto**

**It can connect to many different "big data" databases and data stores at once, and query across them**

### **Hue**

**Graphical front-end for applications on your EMR cluster** 

**Ganglia** (**monitoring** like cloudwatch) 

### **Question 2** 

Which one of the following statements is NOT TRUE regarding EMR Notebooks? 

* EMR notebook is stopped if is idle for an extended time 
* EMR Notebooks currently do not integrate with repositories for version control. 
* **EMR Notebooks can be opened without logging into the AWS Management Console** 
* You cannot attach your notebook to a Kerberos enabled EMR cluster 


> To create or open a notebook and run queries on your EMR cluster you need to log into the AWS Management Console. 

**Kerberos**

**Kerberos** is a way of providing strong authentication through **secret key cryptography**.

This is a **network authentication protocol** that ensures that **passwords or other credentials aren't sent over the network in an unencrypted format**


### **Question 3** 

How can you get a history of all EMR API calls made on your account for security or compliance auditing? 

* Using CloudWatch 
* **Using AWS CloudTrail** 
* Using EMR logs 
* Using AWS Gateway 

> CloudTrail integration is one of the ways in which EMR integrates with AWS. 


### **Question 4** 

If you don't want the data on your cluster to be ephemeral, be sure to store or copy it in S3. 

When you delete your EMR cluster, what happens to the EBS volumes? 


* **EMR will delete the volumes once the EMR cluster is terminated.** 
* EBS volumes are preserved 


### **Question 5** 

Which one of the following statements is NOT TRUE regarding Apache Pig? 

* Pig supports interactive and batch cluster types 
* Pig is operated by a SQL-like language called Pig Latin 
* When used with Amazon EMR, Pig allows accessing multiple filesystems 
* **Pig supports access through JDBC** 


****