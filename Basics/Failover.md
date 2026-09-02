problem : how to maintain the availability of a server, or a data base or any component if they fail

solution : using standby's, these standby's are backup server or backup database, or even a load balancer, and they can be active or passive

all the components in a failover management are connected through a network which constantly checks the heartbeat of the primary component

if there is a change in heartbeat or stop of heartbeat, the secondary or standby server takes the place of primary and sends a notification to the technician that the primary server is failed, and it needs to be fixed


strategies : active-active, active-passive
    active-active : all the components in this type of strategy are active, and they share the load, through a load balancer, let's say we have redundant instances of our service, the load balancer sends the request to any server. in this case the failover recovery time is 0, because the load balancer will send that load to other servers

    active-passive : in a active passive cluster, there will be atleast two nodes, and the max can be anything, but atleast one node is passive, this takes the place of some other, whenever a nodes heartbeat varies, so there is not load on these nodes initially, only load goes whenever an active node gets replaced. 

Graceful degradation in fault tolerance :
    it is economically suitable to allow only some services to the users when some disaster happens, then to have the complete functionality

Fault tolerance :
    node level : we can have multiple nodes of the same application, or db in the same availability zone

    availability zone level : we can have our clustor of servers or databases in multiple zones within a colud region

    region : if the entire region is down, we can have our clustor in multiple regions

    cloud provider : if the entire cloud provider like aws is down, we can have our application in multiple cloud providers like azure 