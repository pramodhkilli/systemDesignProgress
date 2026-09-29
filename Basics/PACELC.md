# PACELC theorem

cap theorem talks about the special case, but it is incomplete and doesnt talk about the overall scenario

so, lets say there is a system, and you have multiple replicas of your db, and if there is a partition, then we have to choose between availability or consistency, what if there is no partition, everything is working fine, every db is reachable and can communicate with the server

then it is not about availability or consistency, it is about latency or consistency

this is what PACELC theorem states

if Partition -> Availability or Consistency
Else -> Latency or Consistency

consider a system where you have 3 read replicas and you dont have a partition in your system, then if a write comes, then what is your strategy, will you write to all the replicas and return the response, which is consistent, or would you choose return the response immediately after writing to the first node, and accept eventual consistency, this case the latency will be low

this depends on the critical parts of the system, where there is a critical thing involved which is limited or scarce which could not be replicated, like money, inventory, or seats in a theatre then we will choose strong consistency, otherwise we will choose low latency
