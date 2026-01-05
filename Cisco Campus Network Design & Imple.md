### **Cisco Campus Network Design \& Implementation**

#### Overview



This project demonstrates the **design, implementation, and troubleshooting of a resilient campus network** using Cisco multilayer switches and a router.

The network was built from the ground up with a strong emphasis on **high availability, scalability, and structured enterprise design.**



Rather than focusing only on device configuration, this project highlights **architectural decisions, failure handling, and systematic troubleshooting**, reflecting real-world network engineering practices.



#### Project Objectives



The primary objectives of this project were to:



* Implement centralised VLAN management across multiple switches



* Provide fault-tolerant default gateways for end devices



* Aggregate links to increase bandwidth and eliminate single points of failure



* Enable inter-VLAN routing at the distribution layer



* Deploy dynamic routing between the campus and the router



* Deliver IP addressing using centralised DHCP with relay across VLANs



* Verify end-to-end connectivity and network resilience



#### Network Architecture



The network follows the Cisco hierarchical network model, separating responsibilities into logical layers.



#### Access Layer



* Provides direct connectivity for end devices (PCs)



* Enforces VLAN membership



* Minimises broadcast domains



#### Distribution Layer



* Aggregates access switches



* Performs inter-VLAN routing using SVIs



* Provides default gateway redundancy using HSRP



* Acts as the policy and control boundary



#### Routing Layer



* Provides centralised network services (DHCP)



* Exchanges routes dynamically using OSPF



* Represents upstream or core connectivity



This layered approach improves scalability, manageability, and fault isolation.



#### Technologies Implemented



The following enterprise networking technologies were implemented:



* **VLANs** for logical network segmentation



* **VTP (Server/Client model)** for centralised VLAN management



* **EtherChannel (Layer 2 \& Layer 3)** for redundancy and increased throughput



* **Inter-VLAN Routing (SVIs)** on multilayer switches



* **HSRP (Hot Standby Router Protocol)** for first-hop redundancy



* **OSPF** for dynamic routing and adjacency formation



* **DHCP** for automated IP address assignment



* **DHCP Relay** (*ip helper-address*) to forward broadcast requests across VLANs



### Implementation Overview

#### Phase 1 – VLAN Management (VTP)



A single multilayer switch was configured as the **VTP Server**, acting as the authoritative source for VLAN information.

All other switches were configured as **VTP Clients**.



This ensured:



* VLANs were created once



* Consistent VLAN propagation across the network



* Reduced configuration errors and administrative overhead



#### Phase 2 – Access Layer Configuration



Access ports were configured in **static access mode** and assigned to their respective VLANs based on departmental requirements.



Key outcomes:



* End devices were correctly segmented



* Broadcast traffic was limited



* PortFast was enabled to improve host convergence time



#### Phase 3 – Link Aggregation (EtherChannel)



EtherChannel was implemented at two levels:



* Layer 2 EtherChannel between access and distribution switches to carry multiple VLANs



* Layer 3 EtherChannel between distribution switches to provide a routed, redundant inter-switch path



This approach:



* Increased available bandwidth



* Eliminated single points of failure



* Simplified spanning-tree behaviour



#### Phase 4 – Inter-VLAN Routing and High Availability



Inter-VLAN routing was enabled on the distribution switches using **SVIs**.



To ensure gateway redundancy:



* **HSRP** was configured



* One switch was made active for VLAN 10



* The other switch was made active for VLAN 11



This provided:



* Continuous default-gateway availability



* Load sharing across VLANs



* Seamless failover in the event of device failure



#### Phase 5 – Routing and Network Services



The router was configured to provide:



* **DHCP services** for all VLANs



* **Dynamic routing** using OSPF



Because DHCP requests are broadcast-based and cannot cross routers, **DHCP relay** was configured on VLAN interfaces using *ip helper-address*.



This allowed:



* DHCP requests from clients to reach the central server



* Proper IP address assignment across all VLANs



#### Verification and Testing



The network was validated using structured verification steps:



* Confirmed VLAN propagation and trunking



* Verified EtherChannel bundling



* Checked HSRP active/standby roles



* Validated OSPF adjacencies



* Confirmed DHCP address assignment



* Tested inter-VLAN connectivity (PC0 ↔ PC3)



All verification steps were successful.



#### Troubleshooting Highlight



During testing, end devices initially received APIPA (169.254.187.30) addresses.



#### Root Cause



* No routing adjacency with the router



* Missing DHCP relay configuration on VLAN interfaces



#### Resolution



* Corrected Layer 3 connectivity



* Implemented ip helper-address on SVIs



#### Lesson Learned



Broadcast-based services such as DHCP require relay configuration in routed environments.

#### 

#### Key Learning Outcomes



* This project reinforced several core networking principles:



* Proper placement of network services is critical



* High availability is achieved through design, not hardware alone



* Layer 2 and Layer 3 failures must be isolated methodically



* Redundancy should be deterministic and predictable



* Verification is as important as configuration



cisco-campus-network-design/

│

├── README.md

├── configs/

│   ├── MLS1.txt

│   ├── MLS2.txt

│   ├── MLS3.txt

│   ├── MLS4.txt

│   └── R3.txt

│

├── diagrams/

│   └── topology.png

│

├── verification/

│   └── verification-commands.txt

│

└── notes/

&nbsp;   └── troubleshooting.md







