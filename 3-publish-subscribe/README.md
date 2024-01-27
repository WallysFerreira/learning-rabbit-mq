# Exchanges

When a producer sends a message to a queue, it actually is not sending them directly to the queue. The message is first sent to an exchange, and then pushed to a queue.

When you declare an exchange you can choose what the exchange is going to do with the message:
- Send it only to the queue that has a binding key that matches the messages's routing key (direct) \{default\}
- (topic)
- (headers)
- Send it to all queues binded to the exchange (fanout)

## Declaring an exchange

To declare an exchange the ExchangeDeclare function on the channel interface is used. It takes as arguments:
- A name for the exchange (name)
- The type of the exchange (type)
- Exchange will survive a server restart (durable)
- Exchange will be deleted when no consumer is listening to it (auto-delete)
- Exchange can only be used by other exchanges (internal)
- Exchange is asynchronous (no-wait)
- X-arguments


# Temporary queues

When using the publish/subscribe pattern, it's good that whenever the server is restarted, queues are emptied out. So queues that are gonna be used by exchanges in this pattern are usually declared with random names and with the 'durable' attribute set to false. When the name attribute is empty, amqp will automatically generate a random name for the queue.

When a consumer disconnects from the queue it should be deleted, so the 'exclusive' attribute is set to true

# Binding queues to exchanges

Using the QueueBind function it's possible to tell the exchange which queue it should push messages to. The function takes as arguments:
- Queue name
- Binding key (routing key)
- Exchange name
- If the operation should be asynchronous (no-wait)
- X-arguments
