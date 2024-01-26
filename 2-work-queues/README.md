# Work Queues / Task Queues

When more than 1 consumer is listening to a queue, RabbitMQ treats them as workers to complete the same task.

By default those workers will share their work in **round-robin** schedule.

# Message acknowledgement

With auto-ack set to true, RabbitMQ doesn't expect a confirmation back from a consumer that the task has been completed, so the message is deleted as soon as it is sent.

To prevent data from being lost because of this, auto-ack can be set to false and then RabbitMQ will expect an acknowledgement to be manually sent.

If a consumer dies before sending an acknowledgement, the server will re-send the message to the queue and another worker will pick it up.

There's a default 30 minutes window that RabbitMQ expects the worker to send an ack back. 

To manually acknowledge a message you can use the function Ack, that requires a boolean argument that says if it's a multi-message acknowledgement.

# Message durability

Turning off auto-ack solves the problem of losing data when a worker is killed before completing a task, but if the entire RabbitMQ server goes down, everything will be lost. Unless the durable property is set to true on queues **and** DeliveryMode is set to amqp.Persisent on messages.

# Fair dispatch

It's possible to tell RabbitMQ to not send a message to a worker that has already been assigned a certain number of tasks using prefetch count.

To set prefetch configurations the Qos function of the channel interface is used. It takes the following arguments:
- Limit of messages a consumer should have at a time (prefetch count) 0 is unlimited
- Limit of size a consumer should be sent at a time in octets (prefetch size) 0 is unlimited 
- Is this change global?
