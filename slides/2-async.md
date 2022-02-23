
# Async communication


## TOC

2.1 Asynchronous workloads

2.2 Message queuing

2.3 Streaming

2.4 Use cases


## Asynchronous workloads

Note:
If we can, we would like to invert how we want to consume data. Instead of a client 
demanding as fast as possible data, we shift this paradigm, and our system is responsible 
to demand more data to process.

With messaging systems, messages are queued asynchronously between client applications and the messaging system.

I will explore two complementary technologies, message queuing and streaming, and how they 
approach and solve asynchronous workloads, and how they can make it possible to 
scale and make services loosely coupled.


![semantics](./slides/assets/semantics.gif)
Note: 
There are different semantics involving delivery messages:

At most once should be used when you want to try to deliver a message,
but you want to guarantee that you won't deliver it twice. A marketing campaign 
might be a good use case for it.

"At-least-once" should be used when you want to guarantee that your message will be processed,
even at the cost of processing it twice. Imagine sending a message to a webchat, that you 
could have an id; if the client received twice the same message and no message in the chat
history can have the same id, the second message can be either ignored or replaced and the application would still behave the same.

Exactly-once delivery is hard to attain, and implementing it transparently and unobtrusively,
 is most likely impossible. Those who claim on doing exactly-once, are doing "effectively-once",
 and either is using some checkpoint engine that reverts when things go wrong or are using some kind of deduplication
 strategy.

To guarantee that the user-defined logic in each operator only executes once per event 
is impossible in the face of arbitrary failures, because partial execution of user code is an ever-present possibility.


## Message queuing
![messaging](./slides/assets/message_queuing.png)

Note:
Message Queuing is unordered or shared messaging.

A message is removed from a queue and then passed to a service's consumer.
This is what we call destructive consumption.

With message queuing, multiple consumers receive messages from a single point-to-point messaging channel.

As shown in the illustration above, when the channel delivers a message, any of the consumers could potentially receive it.

The messaging system's implementation determines which consumer receives the message. 

Queueing systems are ideal for work queues that do not require tasks to be performed in a particular order.

For example, sending one email message to many recipients.RabbitMQ and Amazon SQS are examples of popular queue-based message systems.


## Streaming
![streaming](./slides/assets/streaming.png)

Note:
Streaming is strictly ordered or exclusive messaging.

With streaming messages, only one consumer consumes the messaging channel.

The consumer receives the messages despatched from the channel in the exact order in which they were written.
The green messages are written (in order) to Consumer 0, orange messages to Consumer 1, and purple messages to Consumer 2.

Streaming use cases are usually associated with stateful applications.
Stateful applications care about ordering and their state.

Ordering impacts the correctness of whatever processing logic the application needs to apply when out-of-order consumption occurs.

Streaming works best in situations where the order of messages is important—for example, data ingestion.

Kafka and Amazon Kinesis are examples of messaging systems that use streaming semantics for consuming messages.

With streaming systems, messages are sent in a series, in a sequence - one after the other.
Streams transport messages and the service maintains a pointer or cursor to the message in the stream that it is processing.
The cursor moves across the messages in the stream, advancing each time a message is processed.
Once a message is processed, the service's cursor moves to the next message.
Messages are not removed from a stream to process them.


## Use cases
![use_cases](./slides/assets/use_cases.png)

Note:
So let's discuss when we should use one or another.
As we have seen they are both complementary, each possessing strengths and weaknesses.

Going from the right to the left:
If we need an event history, message queuing is not adequate, as message queues use 
destructive consumption. 

If we need to process events in aggregates, like we need to process a window of data, to 
calculate like an average or anything that depends on previous data, streaming seems more 
appropriate.

Both have topics and subscriptions, but fine-grained subscriptions are more aligned with 
most message queuing system capabilities.

If you are looking for "Once only delivery" semantics, or should I say "effectively-once", you can't go wrong with a message queue.

