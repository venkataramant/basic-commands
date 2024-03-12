# KAFKA
 1. Publish and Subscribe to steram of records like a message queue.
 2. Storage system for messages, can be consumed asynchronously. Kafka writes data to a scalable disk structure and replicates for fault-tolerance. Producers can wait for write knowledgements.
 3. Stream processing with Kafka Streams APIs, enables aggregration/joins of different inputs/streams into an output/stream of processed data.
	
 KAFKA TOPIC (Publish/ Multiple subscribers)
		Every consumer gets all messages and topic still keeps the dlievered messages for future consumption by new/existing consumers.
 KAFKA QUEUE(PTP -Point to Point Messaging system):
		Only one consumer get message and message is deleted once consumer consumes it.
 Advantages:
  1. Loose coupling between producers/consumers
  2. Durability: Messages are stored even consumers are down
  3. Scalability/Fault-tolerance: Producers and Consumers are working in asynchronous mode both of them be scaled up/down as needed
  4. Flexibilty: Can add new Multiple consumers and their functionality can be alerted without distribing other flows.
 Difficulties:
  1. Semantics:
  	 Understanding of the message flow (Topic,partitions and strickiness)
  	 Fallback approach[Reflow of message or Duplicate consuming or Message lost]
  	 	Consumers consume messages by maintaining an offset (or index) to these partitions and reading them sequentially. A single consumer can consume multiple topics, and consumers can scale up to the number of partitions available. As a result, when creating a topic, one should carefully consider the expected throughput of messaging on that topic.
  2. Message Visibility:
  		Debugging multiple consumers and how their handling these messages.
  		Correlatin IDs mybe option.


Feature Set
	Message order
	Message Routing
	Message Timing
		TTL (Time to Live)
		Delayed/Scheduled Messages.
	Message Retention
	Fault Handling
		Transient Failures [Network connectivity/CPU Load/Service Crash...Retry]
		Persistent Failures [Software bugs or invalid message schema]
	Scale
		Kafka uses sequential disk I/O to boost performance. Its architecture using partitions means it scales horizontally (scale-out) better than RabbitMQ, which scales better vertically (scale-up).
	Consumer Complexity
		RabbitMQ uses a smart-broker & dumb-consumer approach. 
		Kafka, on the other hand, uses a dumb-broker & smart-consumer approach. Consumers in a consumer group need to coordinate leases on topic partitions between them (so that only one consumer in a consumer group listens to a specific partition). Consumers also need to manage and store their partitions’ offset index.
	Protocol Compatibility


    RabbitMQ is preferable when we need:
        Advanced and flexible routing rules.
        Message timing control (controlling either message expiry or message delay).
        Advanced fault handling capabilities in cases when consumers are more likely to fail to process messages (either temporarily or permanently).
        Simpler consumer implementations.
    Kafka is preferable when we require:
        Strict message ordering.
        Message retention for extended periods, including the possibility of replaying past messages.
        The ability to reach a large scale when traditional solutions do not suffice.

    For example, in an event-driven architecture-based system, we could use RabbitMQ to send commands between microservices and use Kafka to implement business event notifications. This is because event notifications are often used for event sourcing, batch operations (ETL style), or audit purposes, thus making Kafka very valuable for its message retention capabilities.

    Credit: https://eranstiller.com/rabbitmq-vs-kafka


Active Mq Java (Apache).       PTP Messaging System
Rabbit Mq Erlang (Pivotal Inc) PTP Messaging System/Message Exchanges (Service Bus) [ephemeral and durable subscriptions] [Consumer Groups]

Kafka Java/Scala (Apache)      Publish- Subcriber Message delivery and logging system. Persistence capabilities.

Kafka: Hig Performance monitoring system where losing message is not imporatnt. Producers dont wait for acknowledgements from brokers.Order of messages are guaranteed.

AMQ/RMB: Exactly once delivery and for valuing messages. Lower throughput each delivery state is maintained. Order of messages are not guaranteed.

 Kafka is best used for processing data streams, while RabbitMQ has minimal guarantees regarding ordering messages within a stream. On the other hand, RabbitMQ has built-in support for retry logic and dead-letter exchanges, while Kafka leaves such implementations in the hands of its users.


 RabbitMQ can route messages to subscribers of a message exchange based on subscriber-defined routing rules. A Topic Exchange can route messages based on a dedicated header named routing_key. 

 Kafka does not allow consumers to filter messages on a topic before polling them.A subscribed consumer receives all messages in a partition without exception. 









