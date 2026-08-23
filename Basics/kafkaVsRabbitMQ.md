RabbitMQ :
    more of a traditional messaging queue, where the broker is smart, consumer is simple
    messages comes from producers, and there is some kind of routing logic to route them into their correct queue, and then later these are consumed, and get acknowledgement from consumer, based on the acknowledgement rabbitmq can retry the same task, or remove the task or move it to dead letter queue in case of repeated failures

    ordering : guarantees ordering when there is only single consumer, but when there are multiple the ordering is not guaranteed

    throughput and latency : 4k-10k messages / sec, 1-5ms latency

    message guarantees : at least once

kafka :
    kafka is not a traditional messaging queue, where the broker is simple, consumer is smart
    messages or events come to the broker, and they are sent to different topics, and the consumer consumes however they like to, the whole history, or from the offset of previously traversed messages, kafka keeps these messages based on the configuration which can store it forever, so based on the consumer they can read independently from all the messages irrespective of what other consumer is reading, this is basically done using a pointer called offset which defines till what point messages are read by that particular consumer and incase of any consumer reboot, the consumer resumes from the offset

    ordering : ordering is guaranteed within a partition( each topic has different partitions )

    throughput and latency : 1 million msg/sec, 5-50ms latency

    message guarantees : at least once, exactly once(only kafka to kafka, same cluster, using kafka transactions)