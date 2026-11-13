# Messaging Fundamentals

Model the lifecycle as create, serialize, publish, persist, deliver, process, and acknowledge. Producer, broker, topic/queue/partition, consumer group, offset, business transaction, and ACK each have distinct failure behavior.

Use topic/partition logs for scalable ordered streams and queues for work distribution when that matches the broker. Define retention, replay, schema/versioning, and ownership before implementation.
