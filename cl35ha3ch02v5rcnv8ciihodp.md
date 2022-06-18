## Event-Driven Architecture in Python

Consider you're following your favorite soccer competition via Google's services. For example, if you browse for FCV vs PSG, you'll get the online status from the field. Whatever happens in the game, all users will be notified about it as well. What is the architecture behind these event-based systems? How do companies like Google keep their services aware of the events happening in sports competitions?

In this article, we'll talk about one of the COOLEST architectures you might have seen in web service structures. At the end of the article, we'll be making our theories into realities using an open-source Python project and we will finally dive deeper through the messages.

### 1. What is an Event?
An "Event" is an occurrence that might happen anywhere at any time. When an NBA team hits a three-point in the 4th quarter or when a player shoots a penalty kick in a soccer match at 63' and so on. An architecture that uses events in order to interact with other internal/external services is called an **Event-Driven** architecture. In those systems, almost every action is occurred based on an event. To be more sensible, events cause actions. Just like the electric-based cars that need electricity to be able to work.

### 2. Events Bring Messages
Basically, events get called by either an AI agent or a human. Thinking of an AI agent. There is a camera that holds both goals' lines and calls API endpoints whenever a ball passed each line. Those APIs are interacting with queues and pushing the occurrences as **Messages** to the queues. Each message contains a context that shows what actually happened in the field.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652436501003/XkVjUckum.png align="center")

### 3. Consumers
We figured out that our AI agent produces the message for us. They are responsible for publishing messages to the queues. On the other hand, we got services that are considered as consumers. Just like producers, consumers are interacting with queues as well but the difference is that producers produce the messages through the queues but consumers pull the messages from the queues.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652512365765/3np3Y8k0-.png align="center")

### 4. RabbitMQ
In the Event-Driven systems, there are multiple tools that come in handy in case of designing our systems. Each tool might be useful based on the performance measures that the scenario requires. Some may use [Apache Kafka](https://kafka.apache.org/) and some developers might find [RabbitMQ](https://www.rabbitmq.com/) useful in their case. The idea is the same but the implementation might be different. In this article, we'll talk about RabbitMQ and at the end, we will take a look at a Python project that shows its integrity with an event-based design.

#### 4.1. Message
Message is the context that the producer publishes to the queue so the consumer(s) will be able to access the messages and do some actions based on them. Messages might contain function/method names, parameter values, or even human-readable data types such as JSON.

#### 4.2. Producer
Producer is the agent that publishes the message(s) to the queues. As we talked about earlier, it might be either a human or an AI agent that produces the messages to the queues. In some architectures, you may find multiple producers that are interacting with the different queues based on some routing parameters.

#### 4.3. Consumer
Consumer is the agent that interacts with the queue(s). A consumer can be a mobile application that is running in the background and interacting with queues. Once a message is received by the application, it'll notify the user by showing a popup notification on the screen.

#### 4.4. Queue
Queue acts like an interface between our producer(s) and consumer(s). Queues are the only ways that producers can talk to consumers in.

#### 4.5. Exchange
In RabbitMQ, we have another middleware called Exchange that places right between the producer and queue(s). Since we can have multiple queues in our architecture, producers can interact with the exchange to specify the queue that they want to push the message in. All queues are binned to the exchange using a `binding key`. These binding keys act like addresses to our queues and producers can send a `routing key` to the exchange to specify the path to the queue. Our exchange can route the message in the different ways:

- Direct Exchange
- Topic Exchange
- Fanout Exchange
- Headers Exchange

Since we need only one queue and one route, we are going to use the Direct Exchange in our project. These exchange types are actually different techniques of routing messages to the queues. Most of them are being used in system designs with multiple queues.

### 5. Event-Driven Architecture Open-Source Project
In this open-source project, we'll use [Docker](https://docker.com) in order to set up our RabbitMQ service and expose it to the `localhost` so that we can access the service from the local ports. The project is written in Python. This project is made for educational purposes only. The aim is to make this architecture much easier to understand for audiences and users. 

#### 5.1. Install docker and docker-compose

Use the following tutorials to make `docker` and `docker-compose` ready on your machine.

- [Docker setup guide for Linux, Windows, and Mac users](https://docs.docker.com/get-docker/).
- [Docker-compose installation guide](https://docs.docker.com/compose/install/).

#### 5.2. Clone the project

Open a fresh terminal tab and run the following command.

```shell
git clone https://github.com/lnxpy/event-driven-in-python.git && cd event-driven-in-python
```

#### 5.3. Install the dependencies
You can install the required packages either on your local site-packages or in an [isolated environment](https://docs.python.org/3/library/venv.html).

```shell
pip3 install -r requirements.txt
```

#### 5.4. Start the compose
Make sure your Docker Daemon is working fine and your Docker service is running with the following command on Linux distributions.

```shell
sudo systemctl status docker
```

Then, start pulling the images and run a container in the background.

```shell
docker-compose up -d
```

#### 5.5. Customize the configurations
Open `settings/configs.py` file in a text editor and make changes. The default configuration might be fine for the rest of the project and your tests.

#### 5.6. Start producing and consuming
You can change the variable `MESSAGE` from `settings/configs.py` to make your own message pattern with some additional features like `amount` and `delay`. Once you made your changes, open two fresh terminal tabs and run both `producer.py` and `consumer.py` each after another. Since `producer.py` declares the queue, make sure you run the producer module first. For more message fields, check out `settings/volumes.py`. Make sure you use the exact key name as your message field.

#### 5.7. Preview
We finally reached the end and this is a quick run with the default configurations of the project. As you can see, we are producing the messages to the queue on the left side, and on the other side, we are consuming messages from the queue at the same time. **Unlike this preview, you better run the producer first. I'm running the consumer first because my exchange is already defined and yours might not**.

![2022-05-13_21-08-27.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1652463979306/eav6lFh1x.gif align="center")

[Feel free to have contributions to my project. It needs improvements for sure. I can't make it perfect on my own](https://github.com/lnxpy/event-driven-in-python).

### Conclusion
In this article, we talked about one of the most common architectures on the web. We found out how services keep their clients (consumers) updated and how they handle the different occurrences (events) happening in the real life. And at the end, we stepped way further and realized the concepts in a real project.