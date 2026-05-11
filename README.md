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