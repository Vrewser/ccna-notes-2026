# 1.1 Singe-Area OSPFv2 Concepts

## Introduction to OSPF
__Open Shortest Path First (OSPF)__


<img width="734" height="273" alt="image" src="https://github.com/user-attachments/assets/50117f45-6c7d-4091-8848-f0d274eb11f4" />
<br>



1. OSPFv2 is used for IPv4 networks.
2. OSPFv3 is used for IPV6 networks.

-Root path cost and Rip cost are entirely different things.
-OSPF offers faster convergence and scales to much larger network.

__Dijkstra's algorithm__
-Responsible for computing the cost of each route.

## Components of OSPF
###R outing Protocol Messages
-It uses 5 distinct packet types.
  1. Hello Packet
     -Similar to DHCP discover, but it also maintains connections.
  2. Database Description
     -Checks if two routers' links match.
  3. Link-State Request
     -Requests neighbors for information about missing link details.
  4. Link-State Update
     -The receiving neighbor sends the requested or updated link details.
  5. Link-State Acknowledgement
     -Confirms the update.

### Data Structures
-OSPF uses 3 main data structures.
  1. Adjacency Database
     -Neighbor Table.
     -Lists all connected neighbor routers.
     `show ip ospf neighbor`
  2. Link-State Database
     -Topology Table.
     -This shows the routers and links in the area. Literally topology.
     `show ip ospf database`
  3. Forwarding Database
     -Routing Table.
     -List of routes to be used.
     -Each router is unique and has its own way and location for packets.
     `show ip route`

### Algorithm
-After data structures, the router builds the routing table using the algorithm that's based on Dijkstra to find the shortest possible path.
-The best possible route is then stored into an "SPF tree."

## Link-State Operation
  1.Establish Neighbor Adjacencies
    -A router must have OSPF enabled first
    -OSPF-enabled routers must recognize each other first so that they can share information.
    -The enabled router sends HELLO packets to all the OSPF-enabled routers to see if the links are there.
    -If true, then the enabled router will attempt a _neighbor adjacency._
  2.Exchange LSA
    -Routers then exchange link-state advertisements.
    -LSAs contain the state and cost of each DIRECTLY connected link.
    -Affected neighbors flood the remaining neighbors until each and every one have LSAs.
  3.Build the Link State Database
    -All of topology's information provided by OSPF-enabled routers are stored into a database.
  4.Execute the SPF Algorithm
    -After storing the LSA information, the SPF algorithm is executed and creates the _spf tree_.
  5.Choose the best route.
    -Best paths for each network are offered to the IP routing table.
    -Best paths are determined by the amount of lowest cost to get to the destination.

    
    <img width="639" height="606" alt="image" src="https://github.com/user-attachments/assets/20587840-8fa7-4d4d-9219-6c52bc7b26c6" />
    <br>

    

## Single-Area and Multiarea OSPF
  *Single-Area OSPF
    -All routers are in one area.
    `Best practice to use is area 0.`
  *Multiarea OSPF
    -Uses hierarchy for each areas. 
    -_All areas must connect to the backbone area (area 0)._
    `For example, 10.0.0.2 sits between area 0 and area 2. What's the area called between the areas? **An Area Border Router**.`

## Multiarea OSPF
-Recalculations of the database are kept in an area until updated.
-Too many routers in one area can cause CPU overload, it's best to partition the routers into smaller and manageable areas.

-Route Summarization is not enabled by default.
  `summary-address ip-address mask`
-This reduces the link-state update time by minimizing the areas for processing and memory requirements.
-LSA flooding is stopped per boundaries of the area with multiarea OSPF.


## OSPFv3
-Used mostly for IPv6.
-Supports both IPv4 and IPv6.

*Network Address
  -Referred to as the prefix.
*Subnet Mask
  -Referred to as the prefix-length.

### OSPFv2 and OSPFv3 Data Structures
<img width="847" height="424" alt="Screenshot 2026-08-27 222815" src="https://github.com/user-attachments/assets/ba85a6f7-5d2b-4e3c-8063-60ec063d6300" />
