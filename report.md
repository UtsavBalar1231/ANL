# Smart Campus Network Design Using Cisco Packet Tracer


This report details the design and implementation of a smart campus network utilizing Cisco Packet Tracer, a network simulation tool developed by Cisco Systems. 

The process encompassed software installation, network topology design, device configuration, connectivity testing, and a critical analysis of the design decisions. The objective was to establish a secure and operational network tailored to a campus environment while enhancing practical knowledge of network simulation tools.

---

## **Installation Process**

Cisco Packet Tracer serves as an educational tool for simulating network environments. The software was obtained from the Cisco Netacad website ([www.netacad.com](https://www.netacad.com/)) after registering a free self-learner account, which granted access to the download section. Version 8.2.2, compatible with a 64-bit Windows 10 system, was selected for installation.

The installation proceeded smoothly, following standard procedures such as agreeing to the license terms and specifying the installation directory. System requirements were adequately met, and upon completion, the software launched successfully. A login using Netacad credentials was required, after which the interface presented a range of networking devices and tools available for simulation purposes.

---

## **Network Design**

The network was structured to support a smart campus comprising four key buildings: the student dormitory, faculty offices, library/common areas, and administrative offices. Each building was equipped with a dedicated switch, connected via trunk links to a central core router. This core router interfaced with a firewall router, which in turn linked to an ISP router to emulate internet connectivity.

An IP addressing scheme based on the 192.168.0.0/16 network was adopted to accommodate sufficient address space. Subnets were assigned as follows:

- **Student Dormitory:** 192.168.10.0/24
- **Faculty Offices:** 192.168.20.0/24
- **Library/Common Areas:** 192.168.30.0/24
- **Administrative Offices:** 192.168.40.0/24

VLANs were employed to segment traffic according to user groups, such as students, faculty, and guests. For example, the student dormitory utilized VLAN 10 for students and VLAN 20 for guests, with comparable VLAN setups applied across other buildings to ensure traffic separation and security.

The Open Shortest Path First (OSPF) routing protocol was implemented due to its efficiency in managing traffic within scalable, dynamic networks, thereby supporting potential future expansion of the campus infrastructure.

---

## **Configuration Steps**

Configuration efforts focused on setting up:
- switches
- routers
- wireless access points
to ensure network functionality and security.

### *VLANs and Switches*

Switches in each building were configured with appropriate VLANs. In the student dormitory, for instance:

- VLAN 10 was designated for student devices.
- VLAN 20 was allocated for guest devices.

Ports were assigned to the relevant VLANs based on connected devices, and trunk links were established between switches and the core router to facilitate multi-VLAN traffic.

### *Core Router Configuration*

The core router was configured with subinterfaces to support inter-VLAN routing. For the student dormitory, subinterfaces such as GigabitEthernet0/0.10 (for VLAN 10) and GigabitEthernet0/0.20 (for VLAN 20) were defined, each assigned an IP address within its respective subnet.

OSPF was activated on the core router to enable dynamic routing across subnets. A router ID was established, and pertinent networks were incorporated into the OSPF process to ensure accurate route propagation.

### *Firewall and Internet Access*

A firewall router was positioned between the core router and the ISP router. Network Address Translation (NAT) was configured to convert private campus IP addresses to a simulated public IP (e.g., 203.0.113.1) for internet access.

Access Control Lists (ACLs) were implemented on the firewall to manage traffic. For example, HTTP and HTTPS traffic were permitted, while unnecessary services were blocked to bolster network security.

### *Wireless Configuration*

Wireless access points were installed in each building to provide wireless connectivity. These were configured with SSIDs aligned with the VLANs, such as "Student_WiFi" for VLAN 10 and "Guest_WiFi" for VLAN 20. WPA2 encryption was applied to secure wireless communications.

---

## **Connectivity Tests**

Multiple tests were performed to confirm the network’s operational integrity:

- **Ping Tests:** Successful pings between devices within the same VLAN and across different VLANs verified correct routing configurations.
- **Internet Access:** Devices successfully pinged the ISP router, indicating effective internet connectivity via NAT.
- **Wireless Tests:** Devices connected to designated SSIDs demonstrated communication with other network components and internet access.

Initial testing revealed challenges, such as misassigned VLAN ports, which disrupted communication between some devices. These were addressed by correcting the VLAN assignments.

---

## **Critical Analysis**

The design decisions were assessed for their effectiveness and potential enhancements.

- **Routing Protocol Selection:** OSPF was adopted for its scalability and efficiency in dynamic networks. Although effective, static routing could have offered a simpler alternative for this limited-scale simulation.
- **VLAN Implementation:** VLANs effectively segmented traffic, improving security and organization by isolating user groups.
- **Security Measures:** ACLs and NAT controlled traffic and secured internet access. Additional features, such as a DMZ for public servers or 802.1X authentication, could further enhance security, though their implementation may be constrained within Packet Tracer.
- **Wireless Security:** WPA2 encryption was utilized, though WPA3 could provide superior protection if supported by the tool.

In summary, the project offered practical exposure to network design and configuration principles. The network performed as intended, yet future refinements could incorporate advanced security measures and alternative routing strategies for optimization.

