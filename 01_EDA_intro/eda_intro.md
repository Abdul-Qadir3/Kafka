### **Why use EDA?**
**Loose coupling:** Components are independent and communicate through events, making them easier to develop, maintain, and update.
**Scalability:** EDA can handle increased load by adding more consumers to process events.
**Real-time processing:** Events can trigger actions as they happen, enabling real-time applications.

### **Advantages of EDA**
**Flexibility:** EDA can accommodate changing business needs by adding new event types.
**Resilience:** If one part of the system fails, others can continue processing events.
**Concurrency:** Multiple consumers can process events simultaneously.

### **Disadvantages of EDA**
**Complexity:** Designing and debugging EDA systems can be more complex than traditional architectures.
**Monitoring:** Troubleshooting issues can be challenging due to asynchronous communication.
**Testing:** Testing event-driven systems can require specialized tools and techniques.

### **There are two main approaches to inter-service communication in a microservices architecture:**

**Synchronous Communication:** This method involves a direct call between services, typically using an API exposed by one service that another service can interact with. Protocols like HTTP are commonly used for this purpose. The calling service waits for a response from the other service before proceeding.

**Asynchronous Messaging:** In this approach, services don't directly call each other. Instead, they send messages to a queue or message broker. The receiving service then processes the message independently. This allows for looser coupling between services and improved scalability. Message brokers like Kafka or RabbitMQ are popular choices for asynchronous communication.

**Both synchronous and asynchronous communication have their advantages and disadvantages:**

**Synchronous communication** is simpler to implement and easier to debug, but it can lead to tight coupling between services and performance bottlenecks if not designed carefully.

**Asynchronous communication** offers better scalability and looser coupling, but it can be more complex to implement and reason about.

The **best choice** for your microservices communication will **depend on the specific needs** of your application. Consider factors like latency requirements, message volume, and desired level of coupling between services when making your decision.

## **Kafka 3.7 Docker Image**

**Using Kafka from Console with KRaft Using Docker Image**

Get Kafka supported kafka image from Docker Hub
```bash
docker pull apache/kafka:3.7.0
```
Start the kafka docker container

```bash
docker run -p 9092:9092 apache/kafka:3.7.0
```
Open another console and check to see if container running:

```bash
docker ps
```
Copy the container name, and give the following command to attach:
`Interact with the container`

```bash
docker exec -it <container-name> /bin/bash
```
Note: Kafka commands are in this directory in the container

```bash
/opt/kafka/bin
```
CREATE A TOPIC TO STORE YOUR EVENTS

Kafka is a distributed event streaming platform that lets you read, write, store, and process events (also called records or messages in the documentation) across many machines.

Example events are payment transactions, geolocation updates from mobile phones, shipping orders, sensor measurements from IoT devices or medical equipment, and much more. These events are organized and stored in topics. Very simplified, a topic is similar to a folder in a filesystem, and the events are the files in that folder.

So before you can write your first events, you must create a topic. Open another terminal session and run:
```bash
/opt/kafka/bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092
```
All of Kafka's command line tools have additional options:

Note: run the kafka-topics.sh command without any arguments to display usage information. For example, it can also show you details such as the partition count of the new topic:
```bash
/opt/kafka/bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092
```
Topic: quickstart-events TopicId: NPmZHyhbR9y00wMglMH2sg PartitionCount: 1 ReplicationFactor: 1 Configs: Topic: quickstart-events Partition: 0 Leader: 0 Replicas: 0 Isr: 0

WRITE SOME EVENTS INTO THE TOPIC

A Kafka client communicates with the Kafka brokers via the network for writing (or reading) events. Once received, the brokers will store the events in a durable and fault-tolerant manner for as long as you need—even forever.

Run the console producer client to write a few events into your topic. By default, each line you enter will result in a separate event being written to the topic.

```bash
/opt/kafka/bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
```
This is my first event

This is my second event

You can stop the producer client with Ctrl-C at any time.

READ THE EVENTS

Open another terminal session and run the console consumer client to read the events you just created:

```bash
/opt/kafka/bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
```
This is my first event

This is my second event

You can stop the consumer client with Ctrl-C at any time.

Feel free to experiment: for example, switch back to your producer terminal (previous step) to write additional events, and see how the events immediately show up in your consumer terminal.

Because events are durably stored in Kafka, they can be read as many times and by as many consumers as you want. You can easily verify this by opening yet another terminal session and re-running the previous command again.

# Kafka UI
This is a popular open-source web UI specifically designed for viewing Kafka topics, messages, brokers, consumer groups, and even lets you create new topics. It's known for being lightweight, easy to set up, and supports secure connections. You can find the project on Github here:

```bash
docker network create -d bridge kafka-net

docker network ls

docker run -p 9092:9092 --network kafka-net --name mykafka apache/kafka:3.7.0

docker run -it -p 8080:8080 --network kafka-net -e DYNAMIC_CONFIG_ENABLED=true provectuslabs/kafka-ui
```
In order to integrate kafka broker with kafkaUI use container name in the host

