# 1.1 Single-Area OSPFv2 Concepts

## Introduction to OSPF
**Open Shortest Path First (OSPF)**

![OSPF Terms Table](https://github.com/user-attachments/assets/50117f45-6c7d-4091-8848-f0d274eb11f4)

* OSPFv2 is used for IPv4 networks.
* OSPFv3 is used for IPv6 networks.
* Root path cost and RIP cost are entirely different things.
* OSPF offers faster convergence and scales to much larger networks.

**Dijkstra's Algorithm**
* Responsible for computing the cost of each route.

---

## Components of OSPF

### Routing Protocol Messages
OSPF uses 5 distinct packet types:

1. **Hello Packet**
   * Similar to a DHCP discover packet, but it also maintains routing connections.
2. **Database Description (DBD)**
   * Checks if two neighboring routers' links match.
3. **Link-State Request (LSR)**
   * Requests neighbors for information about missing link details.
4. **Link-State Update (LSU)**
   * The receiving neighbor sends the requested or updated link details.
5. **Link-State Acknowledgement (LACK)**
   * Confirms the successful receipt of the update.

### Data Structures
OSPF relies on 3 main databases:

1. **Adjacency Database** (Neighbor Table)
   * Lists all connected neighbor routers.
   * Command: `show ip ospf neighbor`
2. **Link-State Database** (Topology Table)
   * Displays all routers and links in the area (the complete topology map).
   * Command: `show ip ospf database`
3. **Forwarding Database** (Routing Table)
   * The actual list of routes currently used to forward traffic. Each router's table is unique.
   * Command: `show ip route`

### Algorithm
* After populating the databases, the router calculates paths using Dijkstra's algorithm to determine the shortest possible route.
* The optimal routes are then stored directly into an **SPF tree**.

---

## Link-State Operation

1. **Establish Neighbor Adjacencies**
   * A router must have OSPF enabled.
   * OSPF-enabled routers must recognize each other before sharing information.
   * The router sends **HELLO** packets out its interfaces. If a neighbor responds, they attempt to establish a *neighbor adjacency*.
2. **Exchange LSAs**
   * Routers exchange Link-State Advertisements (LSAs).
   * LSAs contain the exact state and cost of each **directly connected** link.
   * Affected neighbors flood these updates to all other neighbors until the entire network is synchronized.
3. **Build the Link-State Database (LSDB)**
   * All structural network data provided by the LSAs is aggregated inside the local database.
4. **Execute the SPF Algorithm**
   * The router processes the LSDB maps through the SPF algorithm to create the definitive **SPF Tree**.
5. **Choose the Best Route**
   * The shortest paths to each destination network are inserted directly into the local IP routing table.

![R1 SPF Tree Content](https://github.com/user-attachments/assets/20587840-8fa7-4d4d-9219-6c52bc7b26c6)

---

## Single-Area and Multiarea OSPF

* **Single-Area OSPF:** All routers reside within a single area. Best practice is to use **Area 0**.
* **Multiarea OSPF:** Organizes the network into hierarchical components. 
  * *Crucial Rule:* **All areas must connect to the backbone area (Area 0).**
  * *Example:* If a router sits between Area 0 and Area 2, that device is called an **Area Border Router (ABR)**.

---

## Multiarea OSPF Architecture
* Database recalculations are isolated inside their specific area until globally synchronized.
* Growing an area too large causes CPU overload; partitioning routers into smaller, manageable areas optimizes resources.
* **Route Summarization** is disabled by default. It can be enabled using:
  `summary-address ip-address mask`
* Summarization minimizes area processing overhead, reduces link-state update delivery times, and limits LSA flooding boundaries.

---

## OSPFv3
* Used primarily for modern **IPv6** deployments (though it can support both IPv4 and IPv6).
* **Network Address:** Referred to as the *prefix*.
* **Subnet Mask:** Referred to as the *prefix-length*.

### OSPFv2 and OSPFv3 Data Structures

![OSPFv2 and OSPFv3 Table Diagram](https://github.com/user-attachments/assets/ba85a6f7-5d2b-4e3c-8063-60ec063d6300)
