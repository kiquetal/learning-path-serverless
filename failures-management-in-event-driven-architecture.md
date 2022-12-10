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


