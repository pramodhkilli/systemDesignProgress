# server less architecture

whattttttt, what the hell do you mean by serverless, where does the application run then????

yeah yeah, i read about serverless just because I had this reaction when i first saw the term

so, its completely misleading, we do have a server but not an isolated server, what the fuck does that mean, lets consider you have an application which has a limited traffic and there are some points of the day, where you see some spikes, so you took and EC2 machine, completely so that you could handle this high spike, but is this efficient, most of the time your server is not experiencing the spike, it is just experiencing at very limited points of time in a day, so why waste all that computation power and money for that

here comes the concept of serverless architecture, so lets consider a server, which is not our dedicated machine, it could be used by other application, not ours, but we could use some of the computation power of that machine to serve our traffic, that is what serverless architecture is, but you might think this server still has to run our service which is continously taking computation power, nahhh, normally our service is idle, when a request comes our application boots, then it starts serving the requests, if the requests become idle, then our application becomes idle

okay looks cool, why not use it for everything??

    1. this seems cool, but there are issues with serverless architecture, first is the boot time

    2. second is if you have an application which gets continuous load, it is economically better to take a seperate machine instead of using serverless

    3. if your processes take longer time to finish like 15 minutes, then serverless is not for you

    4. it becomes extremely difficult to debug something using a serverless architecture

advantages :

    1. coming to the advantages part, you have to pay per request typically time taken by the server to serve your processes

    2. you dont have to take care of the security, or anything related to the server, you serverless provider takes care of those headaches

common vendors for serverless

1. amazon : lambda
2. google : google cloud functions
3. microsoft : microsoft azure functions
4. cloudflare : cloudflare workers
