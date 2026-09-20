# auto complete

the question we are trying to answer is how search auto completes work, when you type something like "res" then google automatically suggests something like restaurant, rest api, based on the popularity or user relevance

almost all products have this feature to make the user experience smoother, re minimize resistance

functional requirements :

1. given a prefix, return top k suggestions
2. suggestions should be ranked by popularity/relevance
3. suggestions should update as search behaviour changes
4. supports millions/billions fo possible search terms

Non-functional requirements :

1. very low latency (ideally < 50ms)
2. very high qps
3. highly available ( eventual consistency )
4. scalable
5. read heavy

deep dive :

okay lets start with the flow, on every new character entered by the user, we call an api, it should return the top k suggestions for that prefix

so the api might look like

GET /autocomplete/{prefix} -> return top k strings

but how do we store the data, we could simply store in some SQL db like postgres, and on every request we can do something like get results for this prefix sorted in popularity and return the top k strings

but problem here is we have a huge qps, there can be millions of requests coming per second, so we should avoid calling the db, instead use something at the server level, and store the data in ram because it would be faster to retrieve, yeah yeah you might think i will use redis, and if the redis lookup fails i will use db, this could work, but reading db is still constly

so the solution is using trie object, the trie node will have children which points to its descendants, and also the top k results stored at every node with that prefix

trie node :
    vector<Trie*> children,
    List<String> suggestions

so if i get something like ama, then i will go to a->m->a, in this node there are top k suggestions, i will simply return the list of strings

this is okay, but how should our updates work, like if i finally hit search on the finished string, the search request goes, there is another api for that the searches and return the results of the search

but i have to store this search as well, so that i could stay up to date with hot topics and if something overtakes some other thing in popularity, i have to show that first, basically to keep the results fresh, i have to update the data, so how will i do that

you might think that i will write to db, and increment the popularity everytime, yeah that will work, but it is still millions of searches per second

i could think smartly here because, there is a high chance of searches to be the same, so i could kind of aggregate these, and keep the number of times it is searched and periodically write to a persistent storage

so i will use kafka to listen to the searches, and i will use flink to aggregate the searches, then periodically i will write to the db

damn this is cool, but we have to update our in memory trie as well, to finish the whole flow, so i could periodically build the trie using another service, which could store the trie object in binary to a object db like s3, and my autocomplete service can periodically get the data from the s3

there could be concerns on how we could scale our auto complete service, cause the trie might become huge, and keeping that data in memory is not ideal, so we could using partitions like a-f goes to s1, then g-k goes to s2, something like that, but there is possibility of having a hot partition, so we might use replication to minimize the load on that server
