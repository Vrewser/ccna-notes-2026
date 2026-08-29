# 1.3 OSPF Operation

---

## OSPF Operational States

1. **Down State**
   * No Hello Packets have been received from any neighbors yet.
   * The router can send Hello packets out to active interfaces, waiting for any response back.
2. **Init State**
   * The router receives a Hello packet from a neighbor.
   * However, the receiving router's own Router ID is not listed yet in the Hello Packet/DBD.
3. **2-Way State**
   * The router receives a Hello packet with its own RID inside the neighbor list.
   * `DR` and `BDR election` takes place in this state.
4. **ExStart State**
   * Before sending any data, they must decide who gets to lead `DR`.
   * The routers prepare to exchange database summaries.
5. **Exchange State**
   * The routers trade `Database Description (DBD)` packets (type 2).
6. **Loading State**
   * Routers actively request and send missing information.
7. **Full State**
   * Routers have *identical Link-State Databases.*
   * Fully synchronized and ready to compute the shortest path routes.
  
---

## Establish Neighbor Adjacencies
* When OSPF is enabled, the router must determine if there is another OSPF neighbor on the link.

1. Down State
   * Doing nothing.
2. Init state
   * Begins handing out hello packets to OSPF routers in the link to discover.
3. Processing and Noting
   * The receiving router (R2) of the Hello Packet and adds the sending router (R1)
4. Two-Way State
   * R1 also receives R2's Hello packet and registers its RID to its list of OSPF neighbors.
