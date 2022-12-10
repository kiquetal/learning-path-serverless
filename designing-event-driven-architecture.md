#### Characteristics

- Decoupled state and code
- Event-driven
- Agnostic language

### Amazon SQS Integration with Lambda


| Characteristics    | Standard     | Fifo                     | 
|--------------------| ------------ |--------------------------|
 | Record Order      | Not guaranteed | Guaranteed  per group ID |
| Delivery           | Messages may be delivered more than once | Messages are delivered once and remain in the queue until a consumer processes and deletes them |
| Transaction Throuhgput | Unlimited messges per second | FIFO queue support up to 300 messages per second, 



#### Step Function

#### Patterns combinations to update state

- Client Polling

![Client Polling](./images/client-polling.png)

Advantages

- Convenient to replace a synchronous flow

Disadvantages

- Add additional latency to the consistency of the data to the client
- Unnecesary work and increased cost for requests that are not needed (nothing changes)


- Webhook pattern with amazon SNS

![Webhook pattern with amazon SNS](./images/webhook-pattern.png)

Advantages

- No polling

Disadvantages

- Client must be able to receive and process the notification


- WebSocket pattern with AWS AppSync

![websocket-appsync](./images/websocket-appsync.png)

Advantages

- Clients receive updates in real time

Disadvantages

- Client must use graphql


### Serverless Data Processing Patterns

- Data processing with Amazon Kinesis

Ingest and processing data in real time

| ShardLImit | Writes  | Reads                                            |
| ---------- | ------- |--------------------------------------------------|
| Rate       | 1000 records per second | 5 transactions per second , up to 10 000 records |
| Data       | 1 mb per second | 2 mb per second                                  |

TOtal shard capacity 

4 000 MB per second = (1000  * )  S
s = shards
s = 4 

### Kinesis Data Stream: 
You need to specify the number of shards

### Kinesis Data Firehose: 
You don´t need to set the number of shards

### Kinesis Data Analytics: 
use SQL to filter records

|   Kinesis Data Stream | Kinesis Data Firehose                                                
| ---------------------- |----------------------------------------------------------------------|
| Write custom consumers, with more targers | The use case of transforming and storing streamingdata is simplified | 
| Order delivery and exactly once delicery is guaranteed | Order not guaranteed, messages could be delivered more than once     |
| Failing messages block the shard until it succeeds | Retry mechanism are available for each delivery target |
| You set the number of shard | You set the data vaolume and the service manages the number of shards |
| Multiple consumers and multiple types of consumers are used| Stream is associated with a single destination |

### Streaming or messaging for data processing

|    Messaging | Streaming                                                                           |
| ----------- |-------------------------------------------------------------------------------------|
| The core entity is an individual message, and messages rates vary | You look at the stream of messages together, and the stream is generally continuous |
| Messages are deleted when they've been consumder | Data remains on the stream for a period of time. Consumers must maintain a pointer  | 
| COnfigure retries and dead-letter queue for failures | A message is retried until it succeds or expires. You must build error handling into your function to bypass a record |

#### Miscelaneous

Kinesis Data Firehose is ideal for ingesting data for storage. It can
also transform data using an AWS lAMBDA function before storing it in

Kinesis Data Firehose streams can only be associated with a single consumer
and the target must be amazon S3, Amazon Redshift, Amazon Elasticsearch Service, or Splunk.

Messaging services like SQS or SNS would be better suited for
processing and responding to individual messages than processing
a stream of data.

Kinesis Data Firehose has built-in retries, Amazon Kinesis Data Streams
does not, bur order is not guaranteed with Kinesis Data Firehose.

