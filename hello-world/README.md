# Basics

- Producer/Publisher: Program that sends messages
- Consumer: Program that receives messages
- Queue: Buffer that stores messages

A program can be a receiver and a producer at the same time.

Many producers can send messages to one queue and many consumers can receive messages from one queue.

After connecting to a RabbitMQ server, a channel is needed as an interface to do things in the server.

# Declaring queues

One of the functions in the channel is QueueDeclare, used to open a queue. It takes as arguments:
- A name for the queue
- Queue can survive a server restart (durable)
- Queue should be deleted when unused (auto-delete)
- Queue can only be used by one connection and is deleted after that connection closes (exclusive)
- Queue is asynchronous (no-wait)
- X-arguments (Queue priorities, length limit and type, for example)

Declaring a queue is idempotent, so, if a queue with the same name already exists, nothing will happen.

# Publishing messages 

To publish messages to a queue, channel provides the functions Publish and PublishWithContext. They take as arguments:
- Exchange name to publish to
- Name of channel to publish to (routing key)
- An error should be returned if the message can't be sent to a queue (mandatory)
- This message should be sent only if it can be received immediately (immediate)
- The payload

# Consuming messages

To consume messages use the function Consume on the channel interface. It takes as arguments:
- Queue name to expect messages from
- Consumer tag to identify this particular consumer. It is unique per channel
- Every message delivered to this message can be considered acknowledged (auto-ack)
- This consumer will access an exclusive queue (exclusive)
- Ignores messages on the same connection (no-local)
- Consumes asynchronously (no-wait)
- X-arguments
