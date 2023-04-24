## About Azure Cosmos DB

[Azure Cosmos DB](https://learn.microsoft.com/en-us/azure/cosmos-db/introduction) is a NoSQL document database service that provides high availability, elastic scalability, and global distribution. It allows developers to store and manage data in a variety of formats, including JSON, BSON, and SQL. One of the key features of Azure Cosmos DB is its ability to provide predictable and consistent performance for applications. This is achieved through the use of [Request Units (RUs)](https://learn.microsoft.com/en-us/azure/cosmos-db/request-units), which are a measure of the throughput capacity of the database.


Over the last few decades the Database Administrators (DBAs) have perfected the art of monitoring and improving throughtputs.  Some of the most common methods to measure throughtput include: 
Transactions per second (TPS): This measures the number of transactions that can be processed per second.
Queries per second (QPS): This measures the number of queries that can be processed per second.
Pages per second (PPS): This measures the number of pages that can be read or written per second.
Bytes per second (BPS): This measures the number of bytes that can be read or written per second.

These do not map one-to-one with Cosmos RUs. This is short summary of our journey with Azure Cosmos throughtput. 
What does Microsoft say about RUs.

## Official literature on RUs



**What are Request Units (RUs)?**

Request Units (RUs) are a measure of the capacity required to perform a specific database operation in Azure Cosmos DB. RUs are used to measure the throughput of the database and are used to provide predictable and consistent performance for applications. RUs are calculated based on the size of the data being queried, the number of documents being returned, and the complexity of the query.

For example, a simple query that returns a single document with a small size will require fewer RUs than a complex query that returns multiple documents with a larger size. RUs are also used to measure the capacity required to perform other operations, such as document writes, updates, and deletes.

**How are RUs Calculated?**

RUs are calculated based on the following factors:

**Data Size**: The size of the data being queried or modified is a significant factor in determining the RUs required for an operation. Larger data sizes require more resources, which means more RUs are needed to complete the operation. 
**Query Complexity**: The complexity of the query being executed also affects the RUs required. Simple queries require fewer resources and fewer RUs, while more complex queries require more resources and more RUs.
**Number of Documents Returned**: The number of documents being returned by the query affects the RUs required. Queries that return fewer documents require fewer resources and fewer RUs, while queries that return more documents require more resources and more RUs.
**Indexing**: The use of indexing can significantly impact the RUs required for an operation. Indexing can speed up queries, but it also requires additional resources and therefore more RUs.
**Provisioned Throughput**: The provisioned throughput capacity of the database also affects the RUs required for an operation. The more provisioned throughput capacity you have, the more RUs you have available to execute operations.
To calculate RUs, Azure Cosmos DB uses a proprietary algorithm that takes into account these factors. The algorithm is designed to provide predictable and consistent performance for applications by ensuring that the database has enough resources to handle the workload. 
    

| RUs      | Performance |Cost |
| ----------- | ----------- |----------- |
| High      |     Good    | High |
| Low   | Bad| Low|  


## 429s a cry for fixing RUs 
How do you know that RUs need to be tweaked? Cosmos SQL API returns code [429 exceptions](https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/troubleshoot-request-rate-too-large?tabs=resource-specific)


Azure Cosmos DB returns 429 when the current aggregate RU's + the RU for a query will exceed the threshold value. For example, if the threshold is 400 (default value) and current queries use 370 RU's and the next query needs 32 RU's to complete, cosmos will reject the query with code 429. If the next query only needs 10 RU's, it will succeed. 1 Second later, the cumulative RU value is reset to zero and the 22 RU query will have succeed. Alongwith 429 Azure Cosmos DB will also return a "x-ms-retry-after-ms" [header](https://learn.microsoft.com/en-us/rest/api/cosmos-db/common-cosmosdb-rest-response-headers) which will contain a number. The application should wait number of milliseconds before retrying the query.


Adding RUs can alleviate some 429s but do not eliminate 429s as RUs are not only memory or CPU, they are also linked to physical partitions. 

### Physical and Logical Partitions

***Physical partitions*** are the actual storage units for data in Azure Cosmos DB. Each physical partition has a maximum size of ***50 GB*** and can support up to ***10,000 Request Units (RUs)per second***. RUs are ***equally*** distributed across physical partitions with a cap of 10K. When an intensive query, say aggregation runs against a partition and uses 10K RUs, the Cosmos DB API starts returning 429s for all other queries.

***Logical partitions*** are logical groupings of data that are stored on one or more physical partitions. Logical partitions are created using a partition key, which is a property of the data that is used to determine which physical partition the data should be stored on. Each logical partition can store ***up to 20 GB*** of data and index information. One logical partition will not span more than one physical partition. Cosmos will automatically manage logical partition to physical partition mapping. When data in a physical partition grows over 50GB, Azure Cosmos DB will move data of one or more logical partitions to another physical partition automatically.
 
## Changing RUs randomly is costly

### Scaling up
Take a scenario where there is 35 GB data and Azure Cosmos DB is provisioned for 20K RUs. RUs are increased from 20K to 200K

***Impact on Physical partitions***:
Azure Cosmos DB has 2 physical partitions for 20K provisioned RUs. When the RUs are increased to 200K, Azure Cosmos DB will create 18 partitions, for a total of 20 partitions, each with a maximum throughput of 10k.

***Impact on Logical partitions***:
Assuming that the logical partitions were split across 2 physical partitions, Azure Cosmos DB sees that 35GB is less than the 50GB it may decide to leave the logical partitions as is.
In effect you end up paying for 18 empty physical partitions. 

***Impact on 429s***:
As the data resides in 2 physical partitions with each partition getting 10K RUs, the 429s persist and the system unresponsive.

### Scaling down
RUs are decreased from 200K to 20K. 

***Impact on Physical partitions***:
Azure Cosmos DB will not scale down the physical partitions. When the RUs are decreased to 20K, Azure Cosmos DB will continute to have 20 partitions each with a maximum throughput of (20K/20) = 1K per partition.

***Impact on Logical partitions***:
The data may continue to reside in 2 physical partitions

 ***Impact on 429s***:
As the data resides in 2 physical partitions with each partition getting 1K RUs, the 429s increase and the system becomes more unresponsive.

### Merge the partitions
[Merge partitions](https://learn.microsoft.com/en-us/azure/cosmos-db/merge?tabs=azure-powershell%2Cnosql) in order to drop empty physical partitions. 
Note: The merge will not work if [analytical store](https://learn.microsoft.com/en-us/azure/cosmos-db/analytical-store-introduction) is enabled.


## Key practises to apply 
1. Keep a track on access patterns. 
    1. Ensure that majority of the queries are in-partition queries. Cross-partition queries are very expensive.
    2. Create appropriate [indexes](https://learn.microsoft.com/en-us/azure/cosmos-db/index-overview). By default Azure Cosmos DB indexes everry propery. These indexes also contribute to the storage limit of the logical partition.

2. Keep track of storage used by the logical partition. Azure Cosmos DB does not allow partition changes on the fly. Data needs to be [migrated](https://devblogs.microsoft.com/cosmosdb/how-to-change-your-partition-key/) when partition changes.

3. Provision RUs as per usage and data storage requirements. Do not run intensive queries like aggregation on containers that UI. This may degrade user experience. Data may need to be replicated in another storage for running analytical queries.

References:
Cosmos [Capacity planner](https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/estimate-ru-with-capacity-planner)
Picking the right [partition key](https://learn.microsoft.com/en-us/azure/cosmos-db/partitioning-overview)
[Hierarchial Partition Keys](https://learn.microsoft.com/en-us/azure/cosmos-db/hierarchical-partition-keys?tabs=net-v3%2Cbicep)
[Cosmos SDK retry with 429s](https://mattruma.com/adventures-with-cosmos-alerting-and-429-status-codes/)

The Azure Cosmos DB [youtube channel](https://www.youtube.com/azurecosmosdb) is a great place to keep track of the latest developments and sneak peek into upcoming features.