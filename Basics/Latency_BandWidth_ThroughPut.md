latency is the time from start of a request to the receiving of the response
many things can add up to latency, network latency, server processing, data base query

throughput = 1/latency
if latency = 10ms
throughput = 1/10ms
           = 100 requests/second


bandwidth, it is the theoritical maximum throughput

bandwidth delay product :
    bandwidth delay product = bandwidth * latency

Example:

Bandwidth: 1 Gbps = 125 MB/s
Latency: 100ms (coast-to-coast US)
BDP: 125 MB/s × 0.1s = 12.5 MB
This means 12.5 MB of data can be traveling through the pipe at any instant. If your TCP window size is smaller than BDP, you will not fully utilize available bandwidth.

we might need to optimize our db, or introduce horizontal scaling, or introduce caching, use of CDNs, geographical placement of servers, protocol upgrades, to reduce latency, in return increases the throughput