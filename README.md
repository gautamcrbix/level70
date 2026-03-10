OSPF Multi-Area Routing Configuration

Objective
To configure OSPF routing between multiple routers using different areas so that all networks can communicate with each other.

Devices Used
	•	3 Routers (Cisco 2911)
	•	2 Switches (Cisco 2960)
	•	2 PCs
	•	Copper Straight Through Cables

Topology Description
PC1 is connected to Switch1. Switch1 is connected to Router1.
Router1 is connected to Router2.
Router2 is connected to Router3.
Router3 is connected to Switch2, and Switch2 is connected to PC2.
Router2 works as the Backbone Router (Area 0).

IP Addressing Table
Device
Interface
IP Address
Subnet Mask
Router1
G0/0
192.168.1.1
255.255.255.0
Router1
G0/1
10.0.0.1
255.255.255.252
Router2
G0/0
10.0.0.2
255.255.255.252
Router2
G0/1
10.0.0.5
255.255.255.252
Router3
G0/0
10.0.0.6
255.255.255.252
Router3
G0/1
192.168.2.1
255.255.255.0
PC1
NIC
192.168.1.10
255.255.255.0
PC2
NIC
192.168.2.10
255.255.255.0
Default Gateway
PC1 → 192.168.1.1 PC2 → 192.168.2.1

Router Configuration
Router1 Configuration

enable
configure terminal

interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown

interface g0/1
ip address 10.0.0.1 255.255.255.252
no shutdown

router ospf 1
network 192.168.1.0 0.0.0.255 area 1
network 10.0.0.0 0.0.0.3 area 0
end


Router2 Configuration

enable
configure terminal

interface g0/0
ip address 10.0.0.2 255.255.255.252
no shutdown

interface g0/1
ip address 10.0.0.5 255.255.255.252
no shutdown

router ospf 1
network 10.0.0.0 0.0.0.3 area 0
network 10.0.0.4 0.0.0.3 area 0
end


Router3 Configuration

enable
configure terminal

interface g0/0
ip address 10.0.0.6 255.255.255.252
no shutdown

interface g0/1
ip address 192.168.2.1 255.255.255.0
no shutdown

router ospf 1
network 10.0.0.4 0.0.0.3 area 0
network 192.168.2.0 0.0.0.255 area 2
end


Verification Commands
Use the following commands to verify OSPF configuration:

show ip ospf neighbor
show ip route
show ip interface brief


Testing
Ping from PC1 to PC2

ping 192.168.2.10

If ping is successful, the network is working properly.

Result
OSPF routing was successfully configured between multiple routers, and communication between different networks was achieved.
