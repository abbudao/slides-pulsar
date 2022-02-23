# Pulsar Overview


## TOC

3.1 Pulsar mission

3.2 Topics

3.3 Producers

3.4 Consumers

3.5 Subscriptions

3.6 Acks and Nacks

3.7 Retention and Expiry

3.8 Readers


## Pulsar mission

Note:
Pulsar's mission is to unify both Streaming and message queuing by providing a 
coherent API for both use cases, and with the flexibility to make your systems depend 
on them interchangeably.


## Topics

persistent://tenant/namespace/topic


![topics1](./slides/assets/topics1.gif)


![topics2](./slides/assets/topics2.gif)


![topics3](./slides/assets/topics3.gif)


![topics4](./slides/assets/topics4.gif)


![topics5](./slides/assets/topics5.gif)

Note:
Topics don't need to be created beforehand and can be consumed by 
a pattern using service discovery.


## Producers

Note: 
Producers can produce messages asynchronously or synchronously. It's up to you, to pick the right usage.


## Consumers
![consumer](./slides/assets/consumer.png)
Note:
Consumers will receive messages according to the subscription that they opted for on a topic.


## Subscriptions


### Exclusive
![exclusive](./slides/assets/pulsar-exclusive-subscriptions.png)


### Failover
![failover](./slides/assets/pulsar-failover-subscriptions.png)


### Shared
![shared](./slides/assets/pulsar-shared-subscriptions.png)


### Key Shared
![key-shared](./slides/assets/pulsar-key-shared-subscriptions.png)


## Acks and Nacks


## Retention and Expiry
![rentetion](./slides/assets/retention-expiry.png)


## Readers  
![reader](./slides/assets/reader.png)
