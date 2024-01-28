# Remote Procedure Call

RPC in RabbitMQ happens in the following way:
- The RPC server declares a queue named  to receive messages on 
- An RPC client sends a message (request) with a queue name to receive the reply on (reply_to) and an identification to know that a reply is destined to them (correlation_id)
- The RPC server receives the message, does some work and sends the reply to the queue specified on the request message (reply_to), with the identification on it (correlation_id)

The same queue can be used to receive multiple RPC replies, that's why an identification is needed. If there were no identification on the reply messages, the RPC client wouldn't know if the message is destined to them or to another client that made some other totally different request.
