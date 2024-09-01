# Azure Event Hubs

Azure Event Hubs is a cloud native data streaming service that can stream millions of events per second, with low latency, from any source to any destination. Event Hubs is compatible with Apache Kafka, and it enables you to run existing Kafka workloads without any code changes.

How it works
Event Hubs provides a unified event streaming platform with time retention buffer, decoupling event producers from event consumers. The producers and consumer applications can perform large scale data ingestion through multiple protocols.

The following figure shows the key components of Event Hubs architecture:

Diagram that shows the main components of Event Hubs.

The key functional components of Event Hubs include:

Producer applications can ingest data to an event hub using Event Hubs SDKs or any Kafka producer client.
Namespace is the management container for one or more event hubs or Kafka topics. The management tasks such as allocating streaming capacity, configuring network security, enabling Geo Disaster recovery etc. are handled at the namespace level.
Event Hub/Kafka topic: In Event Hubs, you can organize events into an event hub or a Kafka topic. It's an append only distributed log, which can comprise of one or more partitions.
Partitions are used to scale an event hub. They are like lanes in a freeway. If you need more streaming throughput, you need to add more partitions.
Consumer applications consume data by seeking through the event log and maintaining consumer offset. Consumers can be Kafka consumer clients or Event Hubs SDK clients.
Consumer Group is a logical group of consumer instances that reads data from an event hub/Kafka topic. It enables multiple consumers to read the same streaming data in an event hub independently at their own pace and with their own offsets.
Throughput units
The throughput capacity of Event Hubs is controlled by throughput units. Throughput units are pre-purchased units of capacity. A single throughput unit lets you:

Ingress: Up to 1 MB per second or 1000 events per second (whichever comes first).
Egress: Up to 2 MB per second or 4096 events per second.
Beyond the capacity of the purchased throughput units, ingress is throttled and a ServerBusyException is returned. Egress does not produce throttling exceptions, but is still limited to the capacity of the purchased throughput units. If you receive publishing rate exceptions or are expecting to see higher egress, be sure to check how many throughput units you have purchased for the namespace. You can manage throughput units on the Scale blade of the namespaces in the Azure portal. You can also manage throughput units programmatically using the Event Hubs APIs.

Throughput units are pre-purchased and are billed per hour. Once purchased, throughput units are billed for a minimum of one hour. Up to 40 throughput units can be purchased for an Event Hubs namespace and are shared across all event hubs in that namespace.

The Auto-inflate feature of Event Hubs automatically scales up by increasing the number of throughput units, to meet usage needs. Increasing throughput units prevents throttling scenarios, in which:

Data ingress rates exceed set throughput units. Data egress request rates exceed set throughput units
Mapping of events to partitions
You can use a partition key to map incoming event data into specific partitions for the purpose of data organization. The partition key is a sender-supplied value passed into an event hub. It is processed through a static hashing function, which creates the partition assignment. If you don't specify a partition key when publishing an event, a round-robin assignment is used.

The event publisher is only aware of its partition key, not the partition to which the events are published. This decoupling of key and partition insulates the sender from needing to know too much about the downstream processing. A per-device or user unique identity makes a good partition key, but other attributes such as geography can also be used to group related events into a single partition.

Specifying a partition key enables keeping related events together in the same partition and in the exact order in which they arrived. The partition key is some string that is derived from your application context and identifies the interrelationship of the events. A sequence of events identified by a partition key is a stream. A partition is a multiplexed log store for many such streams.

In order to make it sequential you need to select the proper partitionKey - If you don't specify a partition key when publishing an event, a round-robin assignment is used. In many cases, using a partition key is a good choice if event ordering is important. When you use a partition key, these partitions require availability on a single node, and outages can occur over time; for example, when compute nodes reboot and patch.

How configure Event Hub in our solution:

To scale the event hub messages, create partition count (lets say partition count : n )for the event hub. Reason is if the consumer applications read the event hub messages then event hub trigger functions can scale up to n-1 instances. Hence messages are to be read and processed very fast due to scaled up instances.
      2. Identify the partition key of the messages and Call SendToPartition() of optum logger standard library.

           Example :







      3.  Create a consumer group for the subscriber of the event hub which is event hub trigger azure functions.

      To clarify the questions what we had, the functions(Consumption and Elastic) were running under different algorithm based on the settings what we had. Please find more detailed analysis below.
 
## Consumption plan vs EP plan scaling options

We discovered that, 
 
Consumption Plan Function app  func-waas-eval-service-pt-eastus was running under target-based scaling (TBS) algorithm.
Elastic plan function app func-waas-pt-eastus was running under Runtime-driven scaling algorithm
 
This means that using the same scaling algorithm on applications in different SKUs shouldn't result in different scaling behavior.
 
Target-based scaling is enabled by default for function apps on the Consumption plan or Premium plans without runtime scale monitoring.
 
If you wish to disable target-based scaling and revert to incremental scaling, add the following app setting to your function app:TARGET_BASED_SCALING_ENABLED: 0
 
Runtime Scale Monitoring : Azure Functions networking options | Microsoft Learn
https://learn.microsoft.com/en-us/azure/azure-functions/functions-target-based-scaling?tabs=v5%2Ccsharp#premium-plan-with-runtime-scale-monitoring-enabled
 
I was able to confirm this one more time with our product team. If runtime scale monitoring is disabled and if the function host version is 4.3.0 and above you would have target based scaling enabled.

In order to use target-based scaling with the Premium plan when runtime scale monitoring is enabled, add the following app setting to your function app:TARGET_BASED_SCALING_ENABLED: 1
 
The EP app uses runtime-driven scaling as opposed to the new target-based scaling algorithm because the EventHubs extension version does not meet the minimum version requirements (5.2.0) as described here: Target-based scaling in Azure Functions | Microsoft Learn 
 
Runtime-driven scaling ) uses an incremental scaling algorithm, meaning it only requests for one additional worker at a time. This means that the EP application will scale out to fewer instances compared to the consumption application scaling out to more instances in the same amount of time with the same amount of load.
 
Based on the current analysis we would like to propose the action plan below.
 
Action Plan:
You need to send message to a namespace rather than partitions which is not handling or distributing the load appropriately.
If you want to achieve the same scaling behavior between both applications, then you will need to either disable runtime scale monitoring on their EP application or update you EventHub extension version to at least 5.2.0 then enable this app setting: TARGET_BASED_SCALING_ENABLED = 1
How to set runtime scale monitoring : Azure Functions networking options | Microsoft Learn
https://learn.microsoft.com/en-us/azure/azure-functions/functions-networking-options?tabs=azure-cli#premium-plan-with-virtual-network-triggers
How to Enable Target Based Scaling : Target-based scaling in Azure Functions | Microsoft Learn
https://learn.microsoft.com/en-us/azure/azure-functions/functions-target-based-scaling?tabs=v5%2Ccsharp#premium-plan-with-runtime-scale-monitoring-enabled
 
 
Note: Please note that Vnet-restricted event sources cannot be accessed and monitored by scale controller, so if the EventHub source is hidden behind a Vnet, then you will have to continue using runtime scale monitoring in order for the scale controller to continue making informed scaling decisions

Sources:

https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability

https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-hubs?tabs=isolated-process%2Cextensionv5&pivots=programming-language-csharp


https://learn.microsoft.com/en-us/azure/architecture/serverless/event-hubs-functions/event-hubs-functions
