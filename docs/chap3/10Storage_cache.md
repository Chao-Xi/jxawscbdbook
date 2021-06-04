# **L4 ElastiCache Overview**

![Alt Image Text](../images//10_1.png "Body image")

## **1、AWS ElastiCache Overview**

1. The same way RDS is to get managed Relational Databases... 
2. ElastiCache is to get managed Redis or Memcached 
3. **<mark>Caches are in-memory databases with really high performance, low latency</mark>** 
4. **Helps reduce load off of databases for read intensive workloads** 
5. Helps make your application stateless 
6. Write Scaling using sharding  Read Scaling using Read Replicas 
7. Multi AZ with Failover Capability 
8. **AWS takes care of OS maintenance / patching, optimizations, setup, configuration, monitoring, failure recovery and backups** 


## **2、Redis Overview** 

* Redis is an in-memory key-value store 
* Super low latency (sub ms) 
* Cache survive reboots by default (it's called persistence)
*  Great to host 
	*  User sessions
	*  Leaderboard (for gaming) 
	*  Distributed states 
	*  Relieve pressure on databases (such as RDS) 
	*  Pub / Sub capability for messaging 

* Multi AZ with Automatic Failover for disaster recovery if you don't want to lose your cache data 
* **Support for Read Replicas** 


## **3、Memcached Overview**


* Memcached is an in-memory object store 
* **<mark>Cache doesn't survive reboots</mark>**  
* Use cases: 
	* Quick retrieval of objects from memory 
	* Cache often accessed objects 

* Overall, Redis has largely grown in popularity and has better feature sets than Memcached. 
* **I would personally only use Redis for caching needs**. 
