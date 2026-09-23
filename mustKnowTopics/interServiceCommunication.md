# Inter service communication

so, people normally know about how a client interact with a server, and how load balancer distributes the load to different servers, but what if one server wants to communicate with some other service

there are two ways to do this

1. synchronous communication :
    in this type of communication, the server sends a tcp request to another server, waits for its response, then continues the remaining logic

    what the fuck does that mean, yeah yeah i get it, vague terms, lets consider a system like instagram, where a user A posts something, and then users b, c, d like that post or comments on that post, now user A should get the notification, these can be two servers, one server has the /like endpoint which registers the likes or comments, and another server sends the notification, one way we can do is, user b clicks the like button, first server gets the api call, then this synchronously call the notification server and wait for it, then return the response with 200 or something

    but synchronous communication is a blocking call, because your first server is waiting for your second server's response, lets say there are a million calls, your first server has to communicate to your second server these many times, andddd the important part if your second service goes down, this creates a cascading effect, which we have to overcome by using circuit breakers

    but on the flip side, synchronous communication is easy, it just call the damn notification server, that is it and we have to consider synchronous communication when the system we are working with has a sensitivity of real time

2. Asynchronous communication :
    okay, another fancy term, how can we deal the above scenario where we have to deal with the notification but we dont have to wait for the notification service's response, we just send a signal that, "hey notification service, we have received this call, just send a notification to them", that is it, it does not wait for the notification services response and continues to do it's work, now how can we implement this, it is easy to say this

    this is where message queue's comes in, we can have publishers which sends some message, and we have consumers which consume this message, and we have topics to group similar kind of messages, so different consumers can consume differt topics, same goes for the producers

    so in our case, our click register service send message to the message broker, message broker stores it in a queue, then our consumer, notification service consumes this, and notification is sent

    the important point to notice here is that after sending message to the message broker, the click register service does not wait for the notification service, i mean it does not interact with the notification service directly anymore, it just gets the response from the message broker

    but on the flip side we are adding more complexity to our system, and message queue is a single point of failure, and when you introduce multiple message brokers in your system it becomes somewhat difficult to debug if something goes wrong

    but modern message brokers have the ability to retry sending messages and they store the history, if required we can use that, in case of analytical kind of duty, this becomes a key
