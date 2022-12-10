#### Migrations considerations

    - Who owns the data
    - Boundary context
    - How it will scale

- What does this application do and how are its components organized?
- How can you break your data needs up based on the command query responsibility segregation (CQRS) pattern?
- How does the application scale and what components drive the capacity you need?
- Do you have schedule-based tasks?
- Do you have workers listening to a queue?
- Where can you refactor or enhance functionality without impacting the current implementation?


#### Fargate vs Lambda

| Fargate | Lambda |
| ------- | -- |
| Lift and shift with minimal rework | Tasks that run less than 15 minutes |
| Longer running proccesses or larger deployment packages | Spiky, unpredictable workloads |
| Predictable, consistent workload | Unkown demand | 
| Need more than 3 gb of memory | Lighter-weigt, application fouces statless computing
| Application with a non https/lister | Simplified IT automation|
| Run side cars with your service | Real-time data processing| 
| Container image portabilidy with docker runtime | Reduced complexity for development and operations| 

#### DataStores

- Amazon S3

    Flexibile object storage
    Data lakes
    Economical state store
    Claim-check pattern
    Filter data retrieved by Lambda

- DynamoDB

    Key/value data store with milisecond response
    Capture change with DynamodbDB streams

- ElasticCache for Redis

    Well suited for things like real-time dashboards
    In-memory data store with sub-milisecond read/write latency

- Quantum Ledge Database

    Model state change in a cryptographically provable manner


### Best Practices

The best practices for serverless applications include:

Don’t reinvent the wheel.
Stay current.
Prefer idempotent, stateless functions.
Don’t just port your code.
Keep events inside AWS services for as long as possible.
Verify the limits of all of the services involved.


