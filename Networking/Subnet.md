# Subnetting

okayy, what is a subnet, and given a network, how can we subnet the network

so, subnetting basically means, dividing our current network into multiple networks by manipulating the network mask

from our given example, my ip address is 192.168.1.0 and my subnet mask is 255.255.255.0

that means i have 256 usable hosts

but wait, i want to divide this into 4 networks, how can i do that

lets represent the subnet mask in binary : 11111111.11111111.11111111.00000000

here 1's represent that the bits are a part of the network portion, zeroes represent the host portion

but if i want to divide this current network into 4 subnets, we need 2 more bits(log 4 base 2)

so the next two bits in the subnet mask should also be taken away

the subnet mask becomes : 11111111.11111111.11111111.11000000

so then what are the ranges of my 4 new subnetworks :

192.168.1.0 - 63
192.168.1.64 - 127
192.168.1.128 - 191
192.168.1.192 - 255

boom, each network can have 64 hosts, but notice here that we can only divide our network into bases of 2, because our subnet must contain continuous zero's, so if we want to divide our network into 5, the minimum we can do is 8 subnets

we can divide our network into variable sized subnets as well, based on the number of hosts we need. pretty cool
