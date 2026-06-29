# How Data Moves Inside a Local Network

## Media Access Control Address (MAC address)

- In early Ethernet networks, MAC addresses were used to identify network interfaces on the same local network segment.
- A MAC address is assigned to a NIC (network interface card) by the manufacturer (but it can also be changed or locally administered in software) and consists of 12 hexadecimal digits (48 bits).
  - First 24 bits:
    - The Organizationally Unique Identifier is assigned by the IEEE to specific hardware manufacturers (like Intel, Apple, or Cisco) to identify the maker.
  - Last 24 bits:
    - A unique extension identifier assigned by the manufacturer itself.
- How did Ethernet frames move in early shared Ethernet networks?
  - This describes early shared-medium Ethernet environments, such as bus Ethernet or hub-based Ethernet.
  - In this kind of network, all hosts on the same shared medium can see the transmitted frame, but only the host with the matching destination MAC address accepts it.
  - In modern switched Ethernet networks, a switch normally forwards known unicast frames only to the port where the destination MAC address is located.
  - When host A (MAC address 00:1A:2B:3C:4D:5E) sends a frame to host B (MAC address 5E:4D:3C:2B:1A:00):
    - Host A sends:
      - Destination MAC address: MAC address of host B (6B)
      - Source MAC address: MAC address of host A (6B)
      - EtherType (2B)
      - Payload (46-1500B)
      - Frame Check Sequence (FCS) / Cyclic Redundancy Check (CRC) (4B)
    - To host B, host C, host D, ...
    - When host B, host C, host D, ... receive the frame, they check whether the destination MAC address is the same as theirs. If it is, they receive it; otherwise, they discard it.

## Address Resolution Protocol (ARP)

- If Host A only knows Host B's IP address, it still needs Host B's MAC address before it can send an Ethernet frame. To solve this problem, we use ARP.
- If Host B is in the same local subnet, Host A uses ARP to find Host B's MAC address.
- If Host B is outside the local subnet, Host A doesn't use ARP to find Host B's MAC address directly. Instead, Host A uses ARP to find the MAC address of the default gateway, and then sends the Ethernet frame to the default gateway.
- ARP is used for IPv4. IPv6 uses Neighbor Discovery instead.
- Basic process:
  1. Host A sends an ARP broadcast request.
  2. All devices on the LAN receive it.
  3. The device with that IP address replies (unicast) with its MAC address.
  4. Host A stores the IP-MAC mapping in its ARP cache.
  5. Later traffic can use that MAC address directly.
- For example:
  - Host A sends an ARP broadcast request:
    - Destination MAC: FF:FF:FF:FF:FF:FF
    - Source MAC: 00:1A:2B:3C:4D:5E
    - EtherType: ARP (0x0806)
    - Payload:
      - Sender MAC Address: 00:1A:2B:3C:4D:5E
      - Sender IP Address: 192.168.1.10
      - Target MAC Address: 00:00:00:00:00:00
      - Target IP Address: 192.168.1.20
  - Then host B replies:
    - Destination MAC: 00:1A:2B:3C:4D:5E
    - Source MAC: 5E:4D:3C:2B:1A:00
    - EtherType: ARP (0x0806)
    - Payload:
      - Sender MAC Address: 5E:4D:3C:2B:1A:00
      - Sender IP Address: 192.168.1.20
      - Target MAC Address: 00:1A:2B:3C:4D:5E
      - Target IP Address: 192.168.1.10

## Switches

- To reduce unnecessary flooding and separate collision domains, we use switches.
- Switches learn from source MAC addresses and record the relationship between ports and MAC addresses.
- Flood unknown destinations: When a switch receives a frame with an unknown destination MAC address, it forwards the frame out all ports except the incoming port within the same VLAN.
- Age out old entries: To solve the problem of a host moving to another port, MAC table entries expire after some time if no frames are seen from that MAC address.

## Virtual Local Area Network (VLAN) and IP routing

### VLAN

- To split one Layer 2 broadcast domain into multiple separate broadcast domains, we use VLANs.
- A VLAN represents a separate Layer 2 broadcast domain on a switch.
- An 802.1Q tagged Ethernet frame contains:
  - Destination MAC address: MAC address of user B (6B)
  - Source MAC address: MAC address of user A (6B)
  - Tag Protocol Identifier (TPID) (2B)
    - The common value is 0x8100.
    - It tells the receiving device that the Ethernet frame contains a VLAN tag.
  - Tag Control Information (TCI) (2B)
    - PCP: priority (3 bits)
    - DEI: drop eligible indicator (1 bit)
    - VID: VLAN ID (12 bits) (1 - 4094)
  - EtherType (2B)
  - Payload (46-1500B)
  - Frame Check Sequence (FCS) / Cyclic Redundancy Check (CRC) (4B)
- Access ports and trunk ports:
  - An access port usually belongs to one VLAN and is commonly used to connect an end host.
    - Frames sent between an end host and an access port are usually untagged.
  - A trunk port can carry traffic for multiple VLANs and is commonly used between switches or between a switch and a router / Layer 3 switch.
    - Frames on a trunk port usually carry an 802.1Q VLAN tag so the receiving device can identify which VLAN the frame belongs to.
- A switch usually keeps MAC forwarding entries scoped by VLAN.
- Traffic between VLANs must be routed by a router or a Layer 3 switch.
- Whether the traffic is allowed depends on routing and access-control policies.
  
### IP routing
