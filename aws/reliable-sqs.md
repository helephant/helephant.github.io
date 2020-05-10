SQS gives you a some very useful tools for designing a system that works reliably:
* doesn't lose messages, even if the processor is forcibly exited while processing the messages
* 

This is advice for standard queues. Not all of it will not be applicable to FIFO queues. 

## Processing the message safely

To process a 
* Read the message, . 
  * SQS will set the status of the message to 
* Process the message
* Delete 

It is really important not to delete the message from SQS until the processing has been completed and the result has been committed somewhere. Otherwise if something catastrophic happens, the process might not complete and the message will be lost. For example, the EC2 instance that the process is running on may suddenly be terminated without giving the process any time to clean up. If this happens, at the end of the [visibility timeout](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-visibility-timeout.html#configuring-visibility-timeout) the message will become available again and another client can pick it up. 

, for example, the EC2 instance that your process is running on suddenly is terminated, 

It is possible for things like the EC2 instance that your process is running  

Even if the process that is handling the SQS has the ability to re-try a failure, .

How does batches of messages affect this?

If you are using a lambda function to process messages from SQS, this pattern is automatically observed. However, it is important to make
* If you return an error, 
  * If more than **X%** of your messages error, lambda will assume that the system is unhealthy and will throttle the number of concurrent lambdas consuming the messages
* If you return a success, the message will be deleted from the queue.

## At-least once

## Visibility timeout


## Redrive policy and DLQ

Standard queues 

Poison pill


## Message expiry

Messages in a queue all expire after the amount of time set in the queue's [MessageRetentionPeriod](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-sqs-queues.html#aws-sqs-queue-msgretentionperiod). This can be set between 1 minute and 14 days. It defaults to 14 days. 

Can be set per message and per queue?

When a message in a SQS queue expires, it will be deleted from the queue. It will not be forwarded on to the DLQ. If you want expired messages to be forwarded to the DLQ, you will need to build the expiry logic into the consumer. 

If this message is in a DLQ, the expiry time will be [based on when the message entered the original queue](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/working-with-messages.html#setting-up-dead-letter-queue-retention), not when it entered the DLQ. For example if the message has a 4 hour rention period and it spends 1 hour in the original queue, it will be deleted after 3 hours in the DLQ.

Message expiry can be a really useful mechanism. 

## Limitations on SQS

* Message size
* In-flight messages 

## Monitoring SQS

