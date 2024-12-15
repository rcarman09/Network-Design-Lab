# Network-Design-Lab
Packet Tracer Lab File: [https://github.com/rcarman09/Network-Design-Lab/blob/main/NetworkDesignLab.pkt](https://github.com/rcarman09/Network-Design-Lab/raw/main/NetworkDesignLab.pkt)

# Lab Info:  

Username on all L2/L3 switches: __ryan__  

Line Console Password: __RyansLab__  

Enable Password: __RyansLab__

### WLC:  

Username: __Admin__  

Password: __RyansLab!__

### WLANS:  

PSK: __RyansLab!__


## Objective  
This Network Design lab was a great opportunity to apply my knowledge from the CCNA and demonstrates a working knowledge of how to build, configure, and test redundant and scalable networks. The goal is also to build a functional lab where all components in the virtual environment are able to communicate with each other.

## Skills Learned
- Designing a resilient and scalable network
- Configuring static and dynamic routing (OSPF) for the LAN
- Implementing a DMZ for servers communicating via the internet
- Configuring routers, switches, and firewalls using Cisco IOS CLI
- Setting up ACLs on the firewalls
- Configure dynamic NAT on perimeter firewalls
- Configure HSRP and LACP on core switches
- Configure DHCP for the LAN
- Configure Cisco VoIP phones
- Setup Wireless Lan Controller, Lightweight Access Points, and wireless clients
- Create appropriate subnets/vlans needed for the network
- Dual Multihomed design at the network perimeter

## Tools Used
- Cisco Packet Tracer for designing and configuring the network

## Technologies Implemented
- __ISP Connectivity__: Two ISPs for redundant internet connectivity.
- __Network Security__: Two Cisco ASA 5500-X series firewalls for enhanced security and redundancy.
- __Network Routing and Switching__: Core switches and firewalls instead of a router, including Catalyst 3850 and 2960 switches.
- __Wireless Infrastructure__: Cisco Wireless LAN Controllers (WLC) and Lightweight Access Points (LAPs).
- __VoIP__: Cisco Voice Gateway for telephony service.
- __VLAN__: VLANs for different types of traffic (Mgt, LAN, WLAN, VoIP, DMZ, Blackhole).
- __EtherChannel__: Link Aggregation Control Protocol (LACP) for link aggregation.
- __STP PortFast and BPDUguard__: Spanning Tree Protocol configurations for port transitions.
- __Subnetting__: Allocating appropriate IP addresses to each network group.
- __Basic Settings__: Hostnames, passwords, banner messages, password encryption, and IP domain lookup.
- __Inter-VLAN Routing__: Enabling communication between devices in different VLANs.
- __Core Switch__: IP addressing for multilayer switches to enable routing and switching functionalities.
- __DHCP Server__: Dynamic IP address allocation from servers in the server farm.
- __HSRP__: High-availability router protocols for redundancy, load balancing, and failover.
- __Static Addressing__: Static IP addresses for devices in the server room.
- __Routing Protocol__: OSPF for advertising routes on the firewall, routers, and multilayer switches.
- __Standard ACL for SSH__: Simple ACL on the VTY line for remote administrative tasks via SSH.
- __Cisco ASA Firewall__: Default static routes, basic settings, security levels, zones, and policies for access control.
- __Final Testing__: Thorough testing to verify proper communication and ensure all configured elements function as intended.

## Implementation Steps
### Step 1: Network Design  

Design the Network Topology:  

Used Cisco Packet Tracer to design the network topology.  

Used a hierarchical design including an access layer and core/distribution (collapsed-core). 2 Cisco ASA-5506-X firewalls were used at the network perimeter. A link from one of the perimeter firewalls was created that branches off to a DMZ. The WLC and Cisco Voice Gateway both branched off from an access layer switch.  

  ![Access Layer Design](https://i.imgur.com/oKMRsVS.png)

  *Ref 1: Access Layer Design for the Network*

  ![Core Layer Design](https://i.imgur.com/fe0NSZp.png)

  *Ref 2: Core Layer Design for the Network*

  ![Perimeter Firewall and DMZ Design](https://i.imgur.com/EWE1Ctw.png)

  *Ref 3: Perimeter Firewall and DMZ Design for the Network*

  ![WLC and Voice Gateway Design](https://i.imgur.com/ve2Dusl.png)

  *Ref 4: WLC and Voice Gateway Design*

### Step 2: Basic Configurations  

Basice Device Configurations:  

Setup basic settings on all access switches and core routers. This include hostnames, usernames, passwords, banner messages, password encryption, setting up a domain, and SSH for remote management.

Configs:

  ![Basice Device Configurations](https://i.imgur.com/S9GYwn0.png)

  *Ref 5: Basic Device Configurations*

   ![Basice Device Configurations](https://i.imgur.com/E90dFvT.png)

  *Ref 6: Basic Device Configurations Cont.*

### Step 3: VLANs and STP  

Configure VLANs and STP:

Created appropriate VLANs for the network and made sure they were configured on all devices. This includes Management, LAN, WLAN, VoIP, INSIDE-SERVERS, and Blackhole VLANs.  

Assigned VLANs to appropriate ports on the switches. Trunk ports were configured on interfaces leading to the L3 switches in the core and the interface leading to the Cisco Voice Gateway. Access ports were configured on interfaces leading towards hosts on the LAN. Unused interfaces on all switches were shutdown and assigned to the blackhole VLAN. 

Configured portfast and bpduguard on access ports leading towards the LAN.

  ![VLAN and STP Configurations](https://i.imgur.com/DAGF2e9.png)

  *Ref 7: VLAN and STP Configurations*

### Step 4: Routing  

Set Up Core Switches:

- Configured core switches for routing and switching functionalities.
  
- Configured interface VLANs on the core switches (1 for each VLAN).
  
  ![Interface VLAN Configuration on CORE-SW1](https://i.imgur.com/RYD6Slu.png)  

  *Ref 8: VLAN Configuration on CORE-SW1*

  ![Interface VLAN Configuration on CORE-SW2](https://i.imgur.com/BmIqb4c.png)  

  *Ref 9: VLAN Configuration on CORE-SW2*

- Configured each layer 3 switch with dynamic routing using OSPF.

  ![OSPF Configuration](https://i.imgur.com/CKewZ6z.png)

  *Ref 10: OSPF Configuration on CORE-SW1*

  ![OSPF Configuration](https://i.imgur.com/iFAsMEw.png)

  *Ref 11: OSPF Configuration on CORE-SW2*

- Bundled 3 gigabit interfaces connecting to 2nd core switch into 1 logical link using LACP. 

  ![Etherchannel Configuration](https://i.imgur.com/dQJoD4p.png)  

  *Ref 12: Etherchannel Configuration*

  ![Etherchannel Configuration](https://i.imgur.com/vl3rhGL.png)

  *Ref 13: Portchannel Configuration*

- Implemented HSRP for redundancy on both L3 switches.

- Configured ip helper-addresses on both L3 switches for routing DHCP traffic.  

### Step 5: Firewall Configuration  

Set Up Cisco ASA Firewalls:

Configured outside and inside interfaces on both firewalls. Since only 1 firewall has a link to the DMZ, only 1 was configured with a DMZ interface.  

Implemented security-level 0 on all outside interfaces and security-level 100 on inside interfaces. A security-level of 70 was configured on the DMZ. 

Configured IP addresses on all interfaces used in the network.  

Configured OSPF and advertised directly connected networks on both firewalls.  

Setup access control lists to allow any icmp traffic, http traffic using tcp, and DNS traffic using both tcp and udp. Allowed traffic to pass from the DMZ to the internal LAN.  

Configured dynamic NAT on both firewalls. The DMZ, LAN, and WLAN are all participating in NAT.

Configured default routes on both firewalls with a next hop IP address set as the ISP. 

Configs:  

  ![Interface Configurations](https://i.imgur.com/V7XdP1G.png)

  *Ref 14: Gigabit Interface Configurations on PERIMETER-FW1*

  ![Interface Configurations](https://i.imgur.com/reeey7t.png)

  *Ref 15: Gigabit Interface Configurations on PERIMETER-FW2* 

  ![NAT Configurations](https://i.imgur.com/yiqL8dV.png)

  *Ref 16: Dynamic NAT Configurations on PERIMETER-FW1*  

  ![NAT Configurations](https://i.imgur.com/EIPOSW4.png)

  *Ref 17: Dynamic NAT Configurations on PERIMETER-FW2*  

  ![ACL Configurations](https://i.imgur.com/OfaQfqj.png)

  *Ref 18: ACL Configurations on PERIMETER-FW1*

 
### Step 6: Wireless Configuration  

Configure Wireless LAN Controllers:

Set up WLC for centralized management of LAPs.  

Setup a PC with an IP in the same subnet as the WLAN to be able to log in to the WLC through the web.  

Created 4 WLANs on the WLC. 1 for employees, 1 for auditors, 1 for corporate, and 1 for guest.  

Each WLAN was configured to use WPA2 and PSK for authentication.  

Each AP was set to use DHCP with a default gateway set in the WLAN

Configs:

  ![WLC HomePage](https://i.imgur.com/SBDWZJ0.png)

  *Ref 19: WLC HomePage*

  ![WLANS](https://i.imgur.com/zxIpdhU.png)

  *Ref 20: WLANS*

  ![Management Interface Configuration on WLC](https://i.imgur.com/o2SHZ9K.png)

  *Ref 21: Management Interface Configuration on WLC*

### Step 7: VoIP Configuration  

Set Up Cisco Voice Gateway:

Created a Voice Vlan for the LAN in which the VoIP phones reside. Made sure the interfaces on each access switch that connected to a VoIP phone was assigned to the voice vlan.

Configured a subinterface on the router with an IP address for the Voice VLAN.   

Configured DHCP on the router specifically for VoIP. The default gateway is set to the Voice Router.  

Configured the maximum number of IP Phones that can be registered on the router to 30  

Configured the maximum number of directory numbers on the router to also be set to 30  

Configured the source IP address to be used for IP phone service to be the same as the gateway's IP address  

Setup auto-assign on all VoIP phones to automatically assign directory numbers to the phones 

Configs:

 ![Subinterface Configuration on Voice Gateway](https://i.imgur.com/mjgfH2h.png)

  *Ref 22: Subinterface Configuration on Voice Gateway*

 ![DHCP Configuration on Voice Gateway](https://i.imgur.com/0qxYVDY.png)

  *Ref 23: DHCP Configuration on Voice Gateway*

  ![Telephony Service Configuration on Voice Gateway](https://i.imgur.com/4NBA4X4.png)

  *Ref 24: Telephony Service Configuration on Voice Gateway*

  ![Directory Number Configuration on Voice Gateway](https://i.imgur.com/nCKN7yP.png)

  *Ref 25: Directory Number Configuration on Voice Gateway*

  ![Ephone Configuration on Voice Gateway](https://i.imgur.com/Bm8YRbJ.png)

  *Ref 26: Ephone Configuration on Voice Gateway*


### Step 8: DHCP and DNS Configuration  

Set Up Servers:

Configured DHCP and DNS servers in the inside zone.  

Made sure DHCP pools were created for each subnet. 

Verified that all hosts using DHCP were getting IP addresses in their respective subnets.

Made sure hostnames were mapped to the DNS server's IP for basic functionality. 

Tested DNS functionality by using the web browser to visit IP addresses using the corresponding hostname.

Configs:

![WLAN Pool Configuration](https://i.imgur.com/T9GRMNG.png)

*Ref 27: WLAN Pool Configuration on DHCP Server*

![WLAN Pool Configuration](https://i.imgur.com/5Oxhclt.png)

*Ref 28: LAN Pool Configuration on DHCP Server*

![WLAN Pool Configuration](https://i.imgur.com/ZcezQ0t.png)

*Ref 29: Management Pool Configuration on DHCP Server*

![DNS Configuration](https://i.imgur.com/ivTEVPD.png)

*Ref 30: DNS Configuration on DNS Server*

![Testing DNS on a Web Browser](https://i.imgur.com/58MRCp6.png)

*Ref 31: Testing DNS on a Web Browser*

### Step 9: Testing and Verification  

Conducted Final Testing:

Verified inter-VLAN communication.  

Tested internet connectivity and firewall rules.  

Ensured proper functioning of DHCP and DNS.  

Ensured VoIP phones can call one another.  

Tested pinging Internet from LAN.

Tested Wireless Connectivity on Clients.
