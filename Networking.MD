## Core concepts of Networking in any System

- DNS
- DHCP
- NAT
- IP'S
- Ports
- NIC

### Real Time use case of above components

- Run ipconfig and check the ip configration of your system.
- By deafult System has two builtIn NIC(network interface cards) is a hardware component that enables commication between  your system(any system) to the network Without NIC you can't communicate the network.

- In my system I have two builtIn adapters those are Wi-Fi Adapter for wireless communications between devices and Ethernet Adapter for cable communication between devices. 
- As I'm using WIFI adapater for wireless commication between devices, I can check the status of the wifi Adapter(NIC), I see below information
    - Ipv4 address of my system (192.168.1.122)
    - Mac Address(pysical address) is unique identifier for system
    - Ipv4 DHCP IPAddress (192.168.1.1)
    - Ipv4 DNS IpAddress (192.168.1.1)
    - Ipv4 Default Gateway (192.168.1.1)
#### Note
- WiFi Router plays a major role in networking. when our system connects to router, router has DHCP service which automatically assigns private Ip to our system. So typically router acts as DHCP server, Software called as DHCP service is running inside the router which will manage assigning the Ip address to the systems. Route has DNS Server setting that comes from ISP.DNS server Address obtain automatically from the router to our system, So System can ping using domain name(google.com) to the google server

#### Switch 
- switch is used to connect Multiple devices within the same network.
#### router
- Router is used to connect two different networks.Home network connects to internet network.

#### Docker Bridge network
- docker bridge network is a network interface(network adapter) to enable the communication with the network. it acts as switch to connect with multiple devices within the same network. it acts as a router to communicate with two different networks. it acts as DHCP sever that assigns Ip addresses to the containers running in the docker. it has DNS server setting as well. Bridge network has pool of IPS(172.17.0.0/16).
- default bridge has no internal DNS functionality, only External DNS works,custom bridge has DNS funcationality we can access VM using domain name.
 - Act As Router
 - Act as Switch
 - Act as DHCP 
 - Includes NAT mechansim
 - PAT (Port adress Translation)
 - By deafault docker container uses the Bridge network.
 - VM has one Network interface card(192.168.0.1) this is a route Ip which the VM is connected, docker which is installed has virtual netwrok interface card( bridge network: (172.16.0.1)). Container which is created from docker bridge, now container has network interface card(virtual enthernetcard: 172.16.0.2).
#### AWS Cloud
- VPC is act as Switch, internetgateway act as router

#### AZure cloud
- Vnet act as switch, vnet gateway act as a router
#### containers internal communication
- container1 wants to communicate with container2, first request goes to the bridge network,bridge network vchecks the pool of Ip that are associated with it, if Ip exits to response back to container2 , now container2 
communicate with container1

#### containers external communication
- when container in one networkA wants to communicate with another networkB, container in Network send request to bridge network , bridge network checks the pool of ips , now ips does exit so it says I dont have ip of another container which is outside of this network.

#### docker functionality
- docker provides functionality which creates a isalted bubble(container)

#### Docker Host network
- container which is created from host network,directly uses the docker server(host) Ip and port number. conatiner will not get any Ip.

#### Docker bridge network
container which is created from bridge network have conatiner Ip and port gets from bridge network. we map the  docker server(host) Ip and port number with container Ip an port.