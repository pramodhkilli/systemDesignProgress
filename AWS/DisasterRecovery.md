# Disaster Recovery

the entire AWS infra is designed with the assumption that failures are inevitable, but given the design is to recover, how fast we recover becomes the question

there are two important metrics to decide what kind of configuration we make to our application, or infact infrastructure to achieve these

1. RTO : Recovery Time Objective, how long can we be down before we recover
2. RPO : Recovery Point Objective, how much data we can afford to loose

smaller RTO means, we need more infrastructure, Replica region should be up and running, which is more costly

smaller RPO means, need more frequent data replication, which is costly

Strategies :

1. Backup and Restore :

    Disaster Recovery region is empty and do not take any traffic, there are no application or DB servers running, only DB backup files are present, if our primary region is down, we kind of take from the latest backup file and continue from there
    here the RTO is more, and RPO is also more, but we can change the frequency of data replication which could increase the cost but compensate with less data being lost between two backup and the actual data

2. Pilot live :

    int the Disaster recovery region keep the database alive(continuous replication from primary) but app server remains off, and DR region do not take any traffic

    in case of a disaster in the primary region, we can boot up our servers in our DR region which might take 10-30 minutes, and the RPO will be smaller cause we are doing live async replication

3. Active-Passive(Warm standby):

    in the DR region, application and data base servers are running, and there is continuous replication of DB just like Pilot live, but the application servers take a small traffic share

    some companies follow something like 1% traffic to DR region ,and see if everything is working fine, important thing here to note is that DR DB act as a READ Replica, if any write traffic comes to this region it might get redirected to the primary region

    some companies follow something like 0% traffic to DR, but time to time to test the DR region by making primary region down and make DR as new primary and serve all traffic from DR to make sure no surprises will encounter in case of actual disaster

4. Active-Active:

    so there is no DR region and primary region anymore, they both are actively up and running and take traffic, DB sync up happens from both regions, but the critical thing here is how we manage DB writes to the same row in both the regions, it depends on the criticality of the data, something like money related or scarce items, we follow different approach

    how to solve the this DB conflict issue :

    1. last write wins : so which ever is the last write, that is being stored, this makes sense if the data is non critical, like a discription of some movie, or something like that, but critical things like money or a scarce items like a seat in a movie theatre, this is not the approach

    2. GEO Sharding : so may be we kind of shard in a way such that request from a user in the region always goes to the same region, instead of going to some far region, so there wont be any writes happening from other regions

    3. Global database : one regions DB acts as a primary, so if write comes from a different region, we would redirect it to the primary region, but this is kind of a active passive strategy
