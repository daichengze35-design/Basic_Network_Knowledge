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

### IP routing and iproute2

- IP routing answers one question:
  - If this host wants to send an IP packet to a destination IP address, where should the packet go next?
- In Linux, the modern toolset for checking IP addresses, routes, neighbors, and routing policy is usually called iproute2.
  - `ip addr`: show or change IP addresses on interfaces.
  - `ip route`: show or change routes.
  - `ip rule`: show or change routing policy rules.
  - `ip neigh`: show or change the ARP / neighbor table.

#### Subnet mask

- For `192.168.1.10/24`:
  - `192.168.1.10` is the IP address.
  - `/24` means the first 24 bits are the network part.
  - The remaining 8 bits are the host part.
  - `/24` is the same as subnet mask `255.255.255.0`.
- To check whether two IPv4 addresses are in the same subnet, compare their network part.
- For example:
  - Host A: `192.168.1.10/24`
  - Host B: `192.168.1.20/24`
  - Both belong to `192.168.1.0/24`, so they are in the same subnet.
  - Host C: `192.168.2.20/24`
  - Host C belongs to `192.168.2.0/24`, so it is not in the same subnet as Host A.

#### Local delivery and gateway delivery

- If the destination IP address is in the same subnet:
  - The host sends the packet directly to the destination host.
  - It uses ARP to find the destination host's MAC address.
- If the destination IP address is outside the local subnet:
  - The host sends the packet to a router, usually called the default gateway.
  - It uses ARP to find the gateway's MAC address, not the final destination's MAC address.

#### Routing table

- A routing table is a list of rules for deciding the next hop.
- A simple routing table may look like this:
  - `192.168.1.0/24 dev eth0 src 192.168.1.10`
    - Traffic to `192.168.1.0/24` is directly reachable through `eth0`.
  - `default via 192.168.1.1 dev eth0`
    - Traffic that does not match a more specific route is sent to `192.168.1.1`.
- Route selection usually follows longest prefix match:
  - `192.168.1.128/25` is more specific than `192.168.1.0/24`.
  - More specific routes win over less specific routes.

#### Routing policy rules

- `ip route` decides routes inside a routing table.
- `ip rule` decides which routing table should be checked.
- In simple hosts, the main routing table is usually enough.
- In more complex hosts, policy routing can choose routes based on:
  - Source IP address
  - Incoming interface
  - Firewall mark
  - Rule priority
- For example:
  - `ip rule add from 10.0.0.0/24 table 100`
  - `ip route add default via 10.0.0.1 dev eth1 table 100`
  - This means traffic whose source IP is inside `10.0.0.0/24` should use routing table `100`.

#### How a Linux host sends a packet

1. It checks the destination IP address.
2. It checks routing policy rules with `ip rule`.
3. It checks the selected routing table with `ip route`.
4. It chooses the route with the longest matching prefix.
5. It decides whether to send directly to the destination host or to a gateway.
6. It checks the neighbor table with `ip neigh`.
7. If the needed MAC address is unknown, it uses ARP.
8. It sends the Ethernet frame to the next-hop MAC address.