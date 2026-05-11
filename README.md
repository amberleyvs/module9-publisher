# Tutorial A: Event-Driven Architecture

**1. How much data will the publisher program send to the message broker in one run?**

The publisher program will send 5 data messages to the message broker in one run.

This happens because the program calls `publish_event` five times. Each call sends one `UserCreatedEventMessage` to the `user_created` queue.

**2. The URL `amqp://guest:guest@localhost:5672` is the same as in the subscriber program. What does it mean?**

The URL `amqp://guest:guest@localhost:5672` is the AMQP connection URL used to connect the publisher to RabbitMQ.

The first `guest` is the username.

The second `guest` is the password.

`localhost` means the RabbitMQ server is running on the same computer.

`5672` is the default RabbitMQ port for AMQP communication.

Because the publisher and subscriber use the same AMQP URL, both programs connect to the same RabbitMQ message broker. This allows the publisher to send messages to RabbitMQ and the subscriber to receive those messages from RabbitMQ.

**Running RabbitMQ as message broker.**
![RabbitMQ Dashboard](images/rabbitmq-dashboard.png)

**Sending and processing event**
![sending-processing](images/sending-processing.png)
In this experiment, I ran RabbitMQ as the message broker, then started the subscriber program so it could listen to the `user_created` queue.

After that, I ran the publisher program using `cargo run`. The publisher sent 5 `UserCreatedEventMessage` events to RabbitMQ. Since the subscriber was already listening to the same queue, it immediately received and processed those messages.

This shows the event-driven architecture flow. The publisher does not communicate directly with the subscriber. Instead, the publisher sends events to RabbitMQ, and the subscriber consumes the events from RabbitMQ.

**Monitoring RabbitMQ Message Chart**
![RabbitMQ Message Chart](images/monitor-chart.png)

When I ran the publisher again, the RabbitMQ chart showed message activity. This happened because every publisher run sends 5 messages to the `user_created` queue.

The chart shows that RabbitMQ receives messages from the publisher and delivers them to the subscriber. If the subscriber processes messages quickly, the queue does not stay full for long because the messages are consumed almost immediately.