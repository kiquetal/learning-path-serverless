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

