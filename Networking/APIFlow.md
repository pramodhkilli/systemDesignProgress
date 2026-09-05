# question : how a api goes through all the layers in network

the 7 layers in osi model are :
    1. Application layer : http, dns
    2. Presentation
    3. session
    4. Transport : TCP, UDP, Ports
    5. Network : IP, ICMP, routing
    6. Data Link : Ethernet, WiFi, MAC, Switches
    7. Physical : Signals, bits, Cables, Radio, Optics

example : /login

    okay, now we know what api to call, do we know how to call it, we just know that login is something there, but we dont know how to call it, this is where the HTTP layer comes in, basically we need to add some headers, and put our data in json - application layer

    okay now, we know what protocol to use, now how to establish a stable connection with the server, which port of the client is the information coming from, what is the destination port, here comes the - Transport layer, TCP 

    TCP handshake is a 3 way handshake, where the client sends a singnal, server acknowledges, then client sends that acknowledgement has received, then only the future communication works, and TCP has a packets concept, basically we number the packets of data by dividing them, and send them, now if any packet gets missed, server can send that missing packets info, and client sends only the missing ones

    okay, till now i know which port the data is coming from, how to avoid missing information, but how do i know that which server to call, i mean, there are millions of machines on the internet, which is the particular machine that my request has to go to ????

    here comes the Network layer, IP addresses, but how do we know the server IP??? we can get it from DNS

    okay, but wait, i know the source IP address, i know the destination ip address, can i send the data directly to the destination, noooooo, ethernet doesn't work IP to IP, it works on MAC to MAC, so it sends the packet of information to the next device in the network through MAC address, and this is done in the - Data link layer

    important : ip addresses can change, so in a network there can be many devices, and sometimes the ip addresses can change, but mac address doesnt change, so, dns gives me mac address, and i will check if this ip is in the same network as my current device, if not, i will use my mac address, and use the address resolution protocol, which broadcasts this destination ip address to surrounding devices through their mac address, and ask them if this ip is present in their network, ultimately it get the destination mac address

    now, i can just send this information over vacuum, i need a medium, that medium can be physical wires, optical wires, or radio signals and this is done in the - Physical layer
