Whenever we are working with a service on which other services might depend upon. Then initially we might think that we will handle everything asynchronously through promises and async-await functions, we need to handle try and catch logic for each service independently and if we use async-await, then also it would run one after the other. Now, if we use fire-and-forget method, then we might run the services parellelly, for eg, we have created a user, then notification and email service would run parellelly and is independent of each other, but still if any service, say email service fails, then it might have no data to retry and run again to send email. So, we want something that lies in between the first master job and other slave jobs, so that when we publish some record somewhere, like some storage, not DB as it would scan through a whole table to fetch the record, increasing the complexity of process, it is being temporarily pushed inside and then consumed by the slave services to complete their job. Now, we also want something to execute retry logics on failed job, at the same time, we also need something like a buffer storage which could store temporarily the record, so that if traffic spikes, then that buffer could manage the record, just like youtube.

Let's say we have a youtube channel and we upload a video, so that upload is being published over the buffer which is youtube, now I reach out to my friends and others to subscribe to my channel to consume my videos. Now, the video I uploaded is being published to queue and then a queue is bound to it, which inserts my video or post inside their feed through consumer.

Now, we have two types of users, content creators and subscribers, if let's say I have 10k of subscribers or less than that, then it would be too easy for someone to insert the post or video into the feed of my subscribers. Now, I have 1M subscribers let's say, then it would be too much difficult to insert the post or video in everyone's feed, so now what should we do? Should we insert data inside the feed of my subscribers, is it feasible to handle inserts to 1M subscribers? I think the best alternative for it is to create a post and allow the subscribers to fetch the records, based on the activity and interaction of subscribers, for eg, Ayush is a celebrity and have 1M subscribers as 1, 2, 3, ... , 1M where based on activity and interaction, we sort the DB and get to the feed of subscribers, for eg, k subscriber get the feed at kth time, 1st one get the feed at 1th time and so on, if they are sorted in the order of 1, 2, 3, ... , 1M.

This whole discussion above is about message queues which act as a buffer, manage events, asynchronous operations, traffic management and even scalability, for eg, there is too much traffic on one service, we can parallelly bind queue to service-2, to manage traffic which works parellelly. I think message queue is the best for building any application. Now, let's see how can we use it:

1. Installing RabbitMQ using docker

```
docker run -d --hostname rabbitmq --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
```

2. Installing library

```
npm install amqp
```

3. Create Connection

```
import amqp from 'amqplib';

export let channel;

export async function connectRabbitMQ () {
  const connection = await amqp.connect("amqp://localhost");
  channel = await connection.createChannel();
  console.log("RabbitMQ Connected");
}
```

4. App.js file

```
import express from "express";
import { connectRabbitMQ, channel } from "./rabbitmq.js";

const app = express();

async function startServer() {
    await connectRabbitMQ();

    await channel.assertExchange("user.events", "fanout", {
        durable: true,
    });

    app.listen(3000, () => {
        console.log("Server Started");
    });
}

startServer();
```

Durable needs to be true here so that an exchange or queue could survive if rabbitmq restarts. Now, what is exchange? There are 3 kinds of exchange mainly:

1. Direct Exchange
In this exchange, we know the exact match, for eg, if user.exchange is given, we assign it a routing key created, so it knows that it needs to bind queue, so it always bind to other services, with user.exchange using that key and perform actions based on that exact match.

2. Fanout Exchange
In this exchange, if any event occurs, then it should be sent to all the services bounded to queue, so it has no routing key and uses "".

3. Topic Exchange
In this exchange, we make use of wildcard characters to exchange messages with respect to wildcard pattern matching, for eg, user.* would allow the operations to be done over all states of user while *.created would allow operations to be done to all creations bounded to queue. Now, we also make use of '#' character which is being used to match pattern based on more than single word that comes, for eg, it could be user.updated.forSecondTime or user.updated.pending.

When someone knows this message queues topic, they can easily build applications without concerning about scalability problems as it is till date a best algorithm to be implemented in order to exchange messages based on routing and inserting records to DB.

The concept that we have discussed doesn't come from learning some crash course or upskilling ourself in some new language or something because if upskilling or learning some crash course defines our progress or success, then we are just learning another algorithm for the sake of learning, but if we learn it out of curiosity on how this world is being built and what was the psychology behind the person implemented this model, we would not apprciate upskilling or learning some crash course for growth, but for knowing another dimension of creation.

Maybe books and youtube tutorials teach us more and improve us as a person, but the dimensions of brain that software engineering opens up is insane. We can't say that this is the final algorithm and nothing else could replace it, it's just we need to think that what problem do we need to solve, for eg, a problem might come if everyone is a celebrity, so now for 1M celebrities, we need to create 1M posts which is too much difficult for us. So, what can we do? Would fanout on read or fanout on write would help us at that time? I think this urge to solve next problem might take us to some creation or innovation, before that it is just all learning and upskilling that we are doing and this becomes another crash course if not understood from problem solving perspective.


















