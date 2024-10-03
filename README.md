How to launch, test this Spring boot application ? 

First install "Docker desktop" and then you can normal just launch main spring boot application. 
If everything is good you should see this messages inside your Spring boot logs. 
" Sending message...
Received <Hello from RabbitMQ!> "  


This guide walks you through the process of creating a Spring Boot application that publishes and subscribes to a RabbitMQ AMQP server.

Before you can build your messaging application, you need to set up a server to handle receiving and sending messages. This guide assumes that you use Spring Boot Docker Compose support. A prerequisite of this approach is that your development machine has a Docker environment, such as Docker Desktop, available. Add a dependency spring-boot-docker-compose that does the following:

Search for a compose.yml and other common compose filenames in your working directory

Call docker compose up with the discovered compose.yml

Create service connection beans for each supported container

Call docker compose stop when the application is shutdown



Spring AMQP’s RabbitTemplate provides everything you need to send and receive messages with RabbitMQ. However, you need to:

Configure a message listener container.

Declare the queue, the exchange, and the binding between them.

Configure a component to send some messages to test the listener.

Spring Boot automatically creates a connection factory and a RabbitTemplate, reducing the amount of code you have to write.

You will use RabbitTemplate to send messages, and you will register a Receiver with the message listener container to receive messages. 
The connection factory drives both, letting them connect to the RabbitMQ server. 
The following listing (from src/main/java/com/example/messagingrabbitmq/MessagingRabbitmqApplication.java) shows how to create the application class:
