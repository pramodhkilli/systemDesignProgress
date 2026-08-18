Consider a story of a application from user 1 to millions of users
server load increases, we need to manage the increasing load without
changing our architecture drastically

scalability :
    Scalability is the ability of a system to handle increased load by adding resources. The key word here is "ability", a scalable system can grow to meet demand without requiring a complete architectural overhaul.

    Measuring Scalability :
        Requests per second (RPS)	Number of API calls the system handles	10,000 RPS
        Concurrent users	Users active at the same time	50,000 concurrent
        Data volume	Amount of data stored or processed	10 TB storage
        Throughput	Data transferred per unit time	1 GB/s
        Query rate	Database queries per second	50,000 QPS
        Message rate	Messages processed through queues	100,000 msg/s

    Performance Under Load :
        1x (baseline)	50ms	Baseline	Normal operation
        2x	55ms	Excellent	Sublinear growth, caching working well
        5x	70ms	Good	System handling load efficiently
        10x	150ms	Acceptable	Linear degradation, predictable
        10x	500ms	Concerning	Superlinear degradation, bottleneck forming
        10x	Timeout	Critical	System at breaking point

    Vertical Scaling (Scale Up) :
        Vertical scaling means adding more power to your existing machines. Instead of adding more servers, you upgrade to bigger ones.

    Horizontal Scaling (Scale Out) :
        Horizontal scaling means adding more machines rather than upgrading existing ones. Instead of one powerful server, you distribute the load across many commodity servers.
    
    Stateless vs Stateful Services :
        In the stateful model, once a user's session is stored on Server 1, all their requests must go to that same server. This creates hotspots and makes it risky to remove servers. In the stateless model, session data lives in a shared store like Redis, so any server can handle any request. The load balancer has complete freedom to distribute traffic.

        To make services stateless:

            Store session data in a shared cache (Redis, Memcached)
            Use tokens (JWT) instead of server-side sessions
            Store uploaded files in object storage (S3) instead of local disk

    Scaling Different Components :
        Application Tier :
            Key strategies:
            Make services stateless
            Use a load balancer to distribute traffic
            Auto-scale based on CPU, memory, or request count
            Deploy across multiple availability zones
        
        Database Tier
            Databases are typically the hardest to scale because they manage state. Unlike application servers, you cannot simply spin up more database instances and put a load balancer in front of them. Data consistency, durability, and transaction isolation all complicate matters.

                1. Read Replicas
                    For read-heavy workloads (which most applications are), create copies of your database that handle read queries
                    Primary handles all writes, replicas receive changes and serve reads.

                    When to use: Read-to-write ratio is 10:1 or higher, and writes are not the bottleneck.

                2. Sharding (Partitioning)
                    When read replicas are not enough, or when write volume exceeds what a single primary can handle, you need to split your data across multiple databases based on a partition key

                    Common sharding strategies:
                    Range-based: Shard by value ranges (A-H, I-P, Q-Z)
                    Hash-based: Hash the key and mod by number of shards
                    Directory-based: Maintain a lookup table mapping keys to shards

                3. NoSQL Databases
                    NoSQL databases like Cassandra, MongoDB, and DynamoDB are designed for horizontal scaling from the ground up:

                    Built-in sharding: Data is automatically distributed
                    Eventual consistency: Trade strong consistency for availability
                    No joins: Data model must accommodate denormalization

        Caching Tier
            Caching reduces load on databases and improves response times. A well-designed cache can handle 100x the throughput of a database, making it essential for high-traffic systems. Redis, for example, can handle 100,000+ operations per second on a single node.

            Cache Scaling strategies:
                Redis Cluster: Automatically partitions data across nodes using hash slots
                Consistent hashing: Distributes keys evenly and minimizes redistribution when nodes are added or removed
                Cache-aside pattern: Application checks cache first, falls back to database on cache miss, then populates the cache
        
        Message Queue Tier
            Message queues are essential for scaling asynchronous workloads. They decouple producers from consumers, allowing each to scale independently, and they buffer traffic spikes so consumers can process at their own pace.

            How queues help scalability:
                Decouple producers and consumers: Scale each independently
                Buffer traffic spikes: Queue absorbs bursts, consumers process at their own pace
                Partition topics: Kafka partitions allow parallel consumption


