# hbase-overview
Why Hbase?
Idempotent overwrite insert out of the box(Htable.put by Key)
We can achive really better performance(if we will need) but this will take a lot of non trivial code.
Auro support from HDP spark lib.(check Phoenix integration, but it’s of for Spark SQl any way)
No problem with schema evolution
One DB for “Save” and “Enrichment” (No need for Memsql and Reddis and HDFS)
Close to real time
No additional code for compaction file on HDFS and additional Spark Job
Still use HDFS
Much easier integration testing compared to HDFS files, no additional layer like Hive or Spark sql.
All data in one place - easy join
Easy migrate to Presto - HDFS Flow, and use Hbase only like speed layer
Less memory usage for Aggregation query (only for Phoenix)
 Linear and modular scaling - same to HDFS but much better then Memsql Or Reddis 
Hbase memory map can be used to speed up enrichment in same way as reddis (http://hortonworks.com/blog/hbase-blockcache-101/)
Possible Analytics
Hive integration (https://cwiki.apache.org/confluence/display/Hive/HBaseIntegration) Not sure about Performance
Spark SQL
Possible usage of Hfile that will avoid any full scan problem
All Spark sql benefits
Phoenix
Statistic collection
Skip scan (for our model where most analytics work with time series is perfect)
Primary Index
Secondary Index
Views  
Multi Tenancy
Easy metrics
Hive Integration.  Available in our 4.8 release (Must be check with Presto)
optimization for time series
Why not ?
A lot of aditionoal code for LoadBalancing regions and split regions 
 Partioniong strategie and performance of quering(aggregation query) strongly depend on  data model: details
Phoenix usage more complex then any other engine for Analytics (Their own SQL and a lot of Hbase scan features)
More Difficult to maintain. ?? compare with what. But default configuration really more difficult that any others in Hadoop ecosystem.
Slow full scan (but fro most cases for our analytics we don't do it, only by time series) and we still can use Spark sql to read from hfile directly (https://github.com/unicredit/hbase-rdd/blob/master/src/main/scala/unicredit/spark/hbase/HFileSupport.scala)
Not realy good with big number of partitions(region per region server) - what make it bad 
The only way to use it with presto it make hive integration https://issues.apache.org/jira/browse/PHOENIX-2743 (3 different techology in chain, i doubt) Presto have https://github.com/prestodb/presto/issues/3992 that can be finished till end of the year. but it's too long?
HDP 2.5 use Phoenix 4.7 which is better to change to 4.8 or even 4.9 and Query Server

In Coclusion.

Hbase is good tools, it ok for our goal, and better in a lot of cases. But their main disadvantages is complexity and strong dependency on data model. 
So i suggest to don't use it on start of project, before we don't know can we achive our goal with less complex tools.
P.S
Any way i prepare some small example that can be measured for performance.  And got more metric for compare. 
