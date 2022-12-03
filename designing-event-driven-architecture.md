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
- 
