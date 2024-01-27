# Direct exchange

In case it's necessary to route messages to different queues depending on something, it's possible to use a exchange of **type direct**.

When a message is passed to a direct exchange, that message is sent only to queues that were binded to the exchange with the 'binding key' value equal to the message's 'routing key' value.

It's possible to bind multiple different queues to one exchange using the same 'binding key' value.