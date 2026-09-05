# Proxy and Reverse Proxy

proxy is a server that is held between your private network and the internet, to act as a filter

imagine you are in india, and you want to access US netflix content, how can you do it?? you can use a proxy

this is just a single scenario, but other uses include :

1. privacy and anonymity : it keeps your ip address safe, and the packets travel on the internet with the proxy's ip address.
2. Access Control : to enforce content restrictions and monitor the internet usage
3. security : they can filter out malicious content and block suspicious sites
4. Improved performance : proxies cache frequently accessed content, redusing the latency and improving load times

in the Contrary reverse proxy is something that acts as a gate between internet and the servers

this helps to keep the servers identity a secret and stops anyone from attacking the servers, and also reverse proxies acts a cache, and respond to some requests even without contacting servers

and with reverse proxies we can also perform load balancing, and also they can filter any malicious requests.

proxies are actually servers, instead of just a hardware piece like router or switch, they can do caching

how does a proxy work in case if you want to access content of US netflix, you set a proxy that has access of US netflix, it accesses the netflix, it gets the response, then it returns that response to us, bypassing any restriction, VPN's work this way as well

then what is the difference between vpn and a proxy
-> vpn creates a encryption tunnel, so basically every packet that is coming from your device undergoes encryption, let's say you are connected to a public wifi like a coffee shop, if without vpn, the router of the coffee shop can access your requests as your requests goes through that, but if we use vpn, your information will be encryption, additionally after the router it goes to the vpn server, and then it will access your requests on behalf of that vpn server
