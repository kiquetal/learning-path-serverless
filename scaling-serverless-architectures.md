#### Scaling best practices

- Separate your application and database
- Take advantage of the AWS Global Cloud Infrastructure
- Identify and avoid heavy lifting
- Montior for percentile
- Refactor as you go

### Key Considerations

- Evalute trade-offs
- Be aware of service limits end to end
- Balanace perfomance requirements, costs, and busines impact
- Build in monitoring

#### Concurrency

- Lambda concurrency is the number of invocations that can be processed in parallel

#### Invocation models

- Synchronous invocation
Concurrency = request rate * average execution time
        





