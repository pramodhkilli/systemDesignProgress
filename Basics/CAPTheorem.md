# CAP

c : consistency
a : availability
c : partition tolerance(in a distributed system having multiple db nodes, we will face partition, i mean there could be some cases where the database nodes may not be able to communicate with each other, so partitions are inevitable)

CAP theorem states that, from these 3, we can only choose 2 at a time, all the 3 is not possible

so, in every system partitions are inevitable, so we get to the question, that which one should we choose from consistency and availability

lets try to understand what consistency really means, consistency states that we want all our users to see the same data at the same time, so whenever a write request comes, it should be written to all the db instances

availability states that, when there is a difference in the data in different db instances, should my product show the data, or not

this becomes critical, we cant achieve these two at the same time

but strong consistency is needed when we have a resource included which is critical, which cant be shared, like a movie ticket(seat is unique, cannot be booked by 2), money( cannot share old balance after a payment, critical), stocks

and if we dont have a requirement of strong consistency, we need availability, because we want our business to run, we dont care if netflix description is different in different devices, it might take time to update but i need to see the series, who cares about the description
