# Comparing tools


## TOC

5.1 Pulsar benefits

5.2 AWS SQS

5.3 AWS SNS

5.4 AWS Kinesis

5.5 Kafka


## Pulsar benefits
![sinks](./slides/assets/benefits_from_web.png)


## AWS SQS

- Only a message queuing plataform
    - Can't replay messages
    - Single consumer to a Queue

- Queue must be created beforehand
- Cost is lower at a lower scale but higher at a higher scale
- Cloud provider lock-in
- Doesn't support nacks*


## AWS SNS
- Only a messaging service
- Both can be used for fanout
- Supports publishers and subscribers but messages are not durable
- Depends on other products to be actually useful


## AWS Kinesis
- Only a streaming service, not ideal for message queuing
- High costs
- Low throughput (5 reads/s per shard)
- Hard to manage
- Bad libraries


## Kafka
- Only a streaming service, not ideal for message queuing
- Scaling is hard
- Not adequate for a huge amount of topics
- Performance (???)
