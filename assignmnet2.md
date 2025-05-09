Minimal Guide: Setting Up a Basic Network in Cisco Packet Tracer
This guide provides a concise walkthrough for setting up a network in Cisco Packet Tracer 8.2 using two 2901 routers (R1 and R2), a switch (SW1), and two PCs (PC1 and PC2).

Step 1: Set Up the Topology

Add Devices:
Place two 2901 routers (R1, R2), one 2950-24 switch (SW1), and two PCs (PC1, PC2) in the workspace.


Connect Devices:
PC1 to SW1: Copper Straight-Through (PC1 FastEthernet to SW1 FastEthernet0/1).
SW1 to R1: Copper Straight-Through (SW1 FastEthernet0/2 to R1 GigabitEthernet0/0).
R1 to R2: Serial DCE (R1 Serial0/0/0 DCE to R2 Serial0/0/0).
R2 to PC2: Copper Straight-Through (R2 GigabitEthernet0/0 to PC2 FastEthernet).




Step 2: Configure Routers (R1 and R2) via CLI
For each router, use the CLI tab to apply these configurations:
Erase and Reload
enable
erase startup-config
reload


Type no if prompted for auto-setup.

Basic Configuration (R1 Example)
enable
configure terminal
hostname T24CS001_R1
banner motd #Unauthorized access is prohibited!#
enable secret secure123
line console 0
password cisco
login
exec-timeout 0 0
logging synchronous
exit
line vty 0 4
password cisco123
login
exit
exit
write memory


Replace T24CS001_R1 with your roll number and router number (e.g., T24CS001_R2 for R2).

Interface Configuration

R1:

configure terminal
interface GigabitEthernet0/0
ip address 192.168.1.1 255.255.255.0
description Connected to SW1
no shutdown
exit
interface Serial0/0/0
ip address 10.0.0.1 255.255.255.252
clock rate 64000
description WAN Link to R2
no shutdown
exit
exit
write memory


R2:

configure terminal
interface GigabitEthernet0/0
ip address 192.168.2.1 255.255.255.0
description Connected to PC2
no shutdown
exit
interface Serial0/0/0
ip address 10.0.0.2 255.255.255.252
description WAN Link to R1
no shutdown
exit
exit
write memory

Static Routing

R1:

configure terminal
ip route 192.168.2.0 255.255.255.0 10.0.0.2
exit
write memory


R2:

configure terminal
ip route 192.168.1.0 255.255.255.0 10.0.0.1
exit
write memory


Step 3: Configure the Switch (SW1)
GUI Configuration

Click SW1, go to Config tab.
Set Hostname: T24CS001_SW1.
In VLAN Database, add:
VLAN 10: PC1_VLAN
VLAN 20: PC2_VLAN


Set FastEthernet0/1: Access mode, VLAN 10.
Set FastEthernet0/2: Trunk mode.

CLI Configuration
write memory


Step 4: Configure PCs

PC1:
Go to Desktop > IP Configuration.
IP: 192.168.1.10, Mask: 255.255.255.0, Gateway: 192.168.1.1.


PC2:
Go to Desktop > IP Configuration.
IP: 192.168.2.10, Mask: 255.255.255.0, Gateway: 192.168.2.1.




Step 5: Test Connectivity

Local Pings:
PC1: ping 192.168.1.1
PC2: ping 192.168.2.1


WAN Ping:
R1: ping 10.0.0.2


End-to-End Ping:
PC1: ping 192.168.2.10
PC2: ping 192.168.1.10




This guide sets up a functional network. Adjust hostnames and passwords as required. Verify connections if pings fail.

