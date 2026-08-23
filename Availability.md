 Availability measures how often your system is operational and accessible to users. A highly available system continues functioning even when individual components fail.

 Availability is not the same as reliability. A system can be highly available (always up) but unreliable (sometimes gives wrong answers). The two properties are related but distinct.

 Availability = Uptime / (Uptime + Downtime)

 The "Nines" of Availability :
    Availability is often described in terms of "nines." Each additional nine dramatically reduces allowed downtime

Availability in Series vs Parallel
    How you combine components dramatically affects overall availability.

Components in Series
    When components are in series, meaning all must work for the system to function, availability multiplies

    Overall = 99.9% × 99.9% × 99.9% = 99.7%

    Each component in the chain reduces overall availability. You started with three components, each at "three nines," but the combined system is below three nines. Add more components in series, and availability keeps dropping

Components in Parallel
    When components are in parallel, meaning any can handle the request, availability improves dramatically:

    For both servers to be down simultaneously, both must fail at the same time:

    Failure probability = 0.1% × 0.1% = 0.0001%

    Availability = 100% - 0.0001% = 99.9999%

    Two servers with 99.9% availability each give you exactly six nines when running in parallel. This is the power of redundancy.

Common failure modes
    Hardware failures
    Software failures
    Network failures
    Human errors

Redundancy: The Foundation of Availability
    Redundancy is the foundational technique behind almost every availability strategy. Having more than one of something means that any single failure leaves at least one working component still able to serve traffic.

    Redundancy means deploying backup components that can take over when primary components fail.

    Active-Passive (Standby)
        Cold standby is cheapest but slowest. The backup server is not running, so failover requires booting the machine, starting services, and potentially restoring data. This might take 5-15 minutes, which is too slow for most production systems but acceptable for disaster recovery.

        Warm standby keeps the backup running and configured, but not actively processing requests. It might be receiving replicated data but is not in the load balancer pool. Failover involves adding it to the pool and possibly promoting it, which takes seconds to a few minutes.

        Hot standby is the most expensive but fastest. The backup is fully synchronized and ready to serve immediately. For databases, this often means synchronous replication where every write is confirmed on both primary and standby before acknowledging the client.

    Active-Active
        In an active-active configuration, all components handle traffic simultaneously. There is no distinction between primary and backup because every node is doing real work.

        When one node fails, the load balancer simply stops sending traffic to it. There is no failover process because the other nodes were already handling traffic. The remaining nodes absorb the additional load.

    Geographic Redundancy
       Availability Zones are the sweet spot for most applications. They provide meaningful isolation (separate power, cooling, and network) while keeping latency low enough for synchronous replication. Most cloud-native applications deploy across at least two AZs.

        Multi-region deployment is necessary for global applications or those requiring disaster recovery from regional events. The challenge is data replication, since synchronous replication across regions adds significant latency. Most multi-region systems use asynchronous replication and accept some data loss in a disaster (typically seconds to minutes of transactions). 

Redundancy must exist at every layer. A redundant app tier in front of a single database does not solve the availability problem.

Patterns combine into resilient designs. Load balancers with health checks, replicated databases with managed failover, queue-based load leveling, and circuit breakers each address a specific failure mode

Redundancy is not free. Match the investment to the business impact of downtime, not to an aspiration of "as many nines as possible."

