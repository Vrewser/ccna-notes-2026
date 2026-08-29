# 1.2 OSPF Packets 
---
## Types of OSPF Packets
* Link-state packets are the tools used by OSPF to help determine the fastest available route for a packet.

1. **Type 1: Hello Packet**
   * Used to establish and maintain adjacency (direct relationship between two devices) with other OSPF-enabled routers.
2. **Type 2: Database Description (DBD) packet
   * Provides a quick summary of the router's database so the neighbor can check what maps it is missing.
3. **Type 3: Link-State Request (LSR) packet
   * Routers can request more information about any entry in the DBD by sending an LSR.
4. **Type 4: Link-state Update**
   * Used to reply to LSRs to provide new information.
5. **Type 5: Link-State Acknowledgement**
   * After the LSU is received, the router sends an acknowledgement to confirm receipt of the LSU.

---

## Link-State Updates
![LSUs Contain LSAs](<img width="661" height="643" alt="image" src="https://github.com/user-attachments/assets/5926105f-c77a-49af-8e98-d8a2c4fa81b6" />)

---

## Hello Packet
* NOTE: Designated Router (DR) and Backup Designated Router (BDR) are not the same as default gateway.
* Uses `Discover OSPF` and `Advertise` for neighbors of the router.
* OSPF Type 1 must elect a *Designated Router (DB)* and *Backup Designated Router (BDR)*.

### Router ID
* Is used with the Hello Packet to uniquely identify the originating router.
