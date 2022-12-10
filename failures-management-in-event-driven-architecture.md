#### Failure management in your code

 One of the key best practices in any API-based application is to capture
 and retry a call whenever possible and to handle errors gracefully when
 a call fails.
 
- Retries
- Backpressure


### Two typs of errors

- Function errors : Errors that occur in your code
- Invocation errors: If request is rejected before the function is invoked

### Synchronous Event Source:

The client must handle the error

### Asynchronous Event Source:

Lambda retries the event
A dead letter queue, failure destination


#### Erroor handling for stream events

- Bisect batch on function error
- Maximum record age in seconds
- On failure destination

#### Failed-event destinations

- SNS
- SQS
- Lambda
- EventBridge

Stream:

- SNS
- SQS

#### Error handling summary by execution model

- Api Gateway (synchronous event source)

      Timeout considerations (30 seconds)
      
      Retries
 
      Error handling

  - Amazon SNS ( asynchronous event source)

        Timeout considerations: Asynchronous event sources do no wait
        for a response from the function's execution. Requests are handed off to
        Lambda, where they are queued and invoked by Lambda.

        Retries: Have a built-in retries. If the function fails, Lambda retries
        two more times. You can set the Retry Attempts to 0 or 1 instead. 

        If Lambda is unable to invoke the function, lambda will continue to 
        try to run the function again for up to 6 hours. Maximum Event Age.

        Amazon SNS has unique retry behaviors among asynchronous events based on its 
        delivery policy for AWS Lambda. It will perform 3 immediate tries, 2 at 1 second apart,
        10 backing off from 1 second to 20 seconds, and 100,000 at 20 seconds apart.

        Error handling: Use Lambda destinations OnFailure option to send
        failures to anther destination for processing. You can also configure
        a dead-letter queue.
  
- Kinesis Data Streams (polling a stream as an event source)

        Timeout consideration: When the retention period for a record expires, the record
        is no longer available to any consumer. The retention period is 24 hours by default. 
        you can configure Maximum Record Age, to tell Lambda to skip processing a data record
        when it has reached its Maxium Record Age.

        Retries: By Default, Lambda retries a failling batch until the
        retention period for a record expires. You can configure
        Maxium Retry Attempts so that your Lambda function will skip
        retrying a bach of records when it has reached the Maxium Retry Attempts.(or
        it has reached the Maxium Record Age)

        Error handling: Configure onFailute destinatioon on your Lambda function
        so that when a data reaches the Maxium Retry Attemps or the Maxium Record Age,
        you can send its metadata, such as shardID and ARN, to an SQS or SNS queue.

        Use BisectBatchOnFunctionError to tell Lambda to split a failed batch
        into two smaller batches and retry each batch separately.

- SQS Queues (polling a queue as an event source)


      
        Timeout considerations – When the visibility timeout expires, messages become visible to other consumers on the queue. 
        Set your visibility timeout to 6 times the timeout you configure for your function.
        Retries – Use the maxReceiveCount on the queue's policy to limit the number of times Lambda will retry to 
        process a failed execution.
        Error handling – Write your functions to delete each message as it is successfully processed. Move failed messages 
        to a dead-letter queue configured on the source SQS queue.

##### Failure management accross your application

- AWS Step Functions

- Amazon SQS

- Amazon SNS

- Aws X-Ray


>As a best practice, ensure that production code can handle Lambda service exceptions
> (Lambda.ServiceException and Lambda.SdkclientException).


#### Failure management with dead-letter queue

You configure the dead-letter queue on the source queue.

| Dead-Letter queue on Lambda function                                                                | Dead-Letter queue on SQS source queue|
|-----------------------------------------------------------------------------------------------------|--------------------------------------|
 | Dead-Letter queue is configured as part of the function                                             | Dead-letter queue is poart of the queu policy|
| Messages that error out after two built-in retries are routed to the dead-letter queue              | The policy describes how many retries before an item is moved to a dead-letter queue | 
| <td colspan=2> Both need a mechanism to redrive messages back to the original source for processing |


#### Distributed tracing with AWS X-ray

- Traces: You've identified failures at an Integration point and want to review
individual requests

- Subsegments: You need a more granular breakout of the work done in a request
to resolve issue

- Service Graph: Customers have reported issues using a servie, and you
need a quick sense of status.

- Annotations: YOu want to be able to group traces accross application, operations
to compare perfomance.



#### Tests



If a Lambda function returns errors when processing messages, 
Lambda decreases the number of processes polling the queue. 
In addition, Lambda has a default of five parallel processes to get things off of a queue.



A best practice is to set your visibility timeout to 6 times the function timeout, not 3 times. 
If the Lambda service detects an increase in queue size,
it will automatically increase how many batches it gets from the queue, each time.
That means it will increase the number of concurrent Lambda functions it invokes. 
Lastly, if the visibility timeout expires before the 
Lambda function has processed the messages in a batch, 
any message in that batch that hasn’t been deleted by your 
function will become visible again.






