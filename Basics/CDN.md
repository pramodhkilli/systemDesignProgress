# CDN

CDN stands for content delivery network, lets understand the problem and why we use content delivery networks

lets say we have a website, which has dynamic data which we might store in some data base, and we also have static data like our html pages, videos, which wont change that much based on the user or location

so is it really mandatory to go to the server everytime to load these, or can we store them in something like a cache to load them faster, and later when user clicks on something, then dynamic data can be loaded, yepp, we can store it somewhere to load faster

this is our CDN

but the think about CDN is it is a single point of failure, so we need to have a distributed CDN nodes, so that we can ensure availability

so what strategy should we use for load balancing here, all the mobile devices goes to some node n1, all the tab devices goes to some node n2 and laptops to n3

but if any node fails, it is still a failure, we could use consistent hashing here to ensure the availability, but think for a second, you can have users around the world, you might want to make the latency minimum, so instead of having all our nodes in a single data centre or location, we could possibly distribute into different locations, such that all users in india are served by a server in india, and so on
