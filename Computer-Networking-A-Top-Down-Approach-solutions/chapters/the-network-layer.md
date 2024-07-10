# Chapter 4: The Network Layer

## Review Questions

### R1.

The name of a network-layer packet is a **datagram**.

### Fundamental Differences between a Router and Link-Layer Switch

| **Aspect**            | **Router**                          | **Link-Layer Switch**              |
|-----------------------|-------------------------------------|------------------------------------|
| **Layer of Operation** | Network layer (Layer 3)             | Data-link layer (Layer 2)          |
| **Functionality**     | Routes packets between networks using IP addresses | Forwards frames within the same network using MAC addresses |
| **Addressing**        | Uses IP addresses                   | Uses MAC addresses                 |


### R2. 

The two most important network-layer functions in a datagram network are **forwarding** and **routing**. 
The three most important network-layer functions in a virtual-circuit network are the same two functions as in a datagram network (**forwarding** and **routing**) and **maintaining connection state information**.


### R3. 

- Forwarding refers to the router-local action of transferring a packet from an input link interface to the appropriate output link interface.
- Routing refers to the network-wide process that determines the end-to-end paths that packets take from source to destination.


### R7. 

The reason each input port in a high-speed router stores a shadow copy of the forwarding table is to allow quick local decisions for forwarding packets. This way, the router doesn't need to send a request to the central processor for each packet, which helps in avoiding delays and minimizing the possibility of bottleneck at the central processor. 


### R8. 

Three types of switching fabrics in a router are: **via memory**, **via a bus**, and **via an interconnection network**.

1. **Switching via Memory:**
    - The input port signals the routing processor when a packet arrives.
    - The packet is copied to the processor's memory.
    - The processor extracts the destination address, looks up the output port, and copies the packet to the output port's buffer.
    - **Limitation:** Only one packet can be processed at a time due to a single memory read/write operation over the shared bus.

2. **Switching via a Bus:**
    - The input port transfers the packet directly to all output ports over a shared bus, without the processor's intervention.
    - Only the output port that matches the destination address accepts the packet.
    - **Limitation:** Only one packet can cross the bus at a time, so packets must wait for their turn.

3. **Switching via an Interconnection Network:**
    - Packets are sent through a crossbar switch with multiple buses.
    - The switch controller manages connections (crosspoints) between input and output ports, allowing multiple packets to travel simultaneously.
    - **Advantage:** Multiple packets can be sent in parallel, provided they don't use the same input or output ports simultaneously.

**Parallel Packet Sending:**
- **Interconnection Network:** This type can send multiple packets across the fabric in parallel.


### R9.

#### Causes of Packet Loss at Input Ports:
1. **Insufficient Switch Speed:** If the switch's transfer rate is less than $N \times R_{\text{line}}$, it can't handle the combined input rate from all ports, leading to the packets being dropped.
2. **Buffer Overflow:** Each input port has a limited buffer size. If packets arrive faster than they can be processed and forwarded (which also means that the switching fabric rate is not high enough), the buffer can overflow, resulting in packet loss.

#### Solutions to Eliminate Packet Loss at Input Ports (without using infinite buffers)
1. **Increase Switch Speed:**
    - Use a switch with a transfer rate at least equal to $N \times R_{\text{line}}$ so that all the packets can be processed and forwarded in negligible time.
2. **Traffic Shaping:**
    - Introduce delays at input ports to smooth out bursts of traffic, giving the switch more time to process incoming packets.


### R10.

### Causes of Packet loss at Output Ports: 
1. **Buffer Overflow:** Each output port has a limited buffer size. When packets arrive at an output port faster than they can be transmitted, the buffer may fill up, causing any additional incoming packets to be dropped. 
2. **Congestion:** In case multiple input ports are sending packets to the same output port simultaneously, it can lead to congestion and buffer overflow of this congested output port, resulting packet loss. 

### Can This Loss Be Prevented by Increasing the Switch Fabric Speed? 
NO. While a faster switch fabric can reduce delays and improve overall throughput, it does not address the root cause of packet loos at the output ports, which is buffer overflow. 


### R11. 

Head-of-the-line (HOL) blocking is a phenomenon that occurs in **input ports** when a packet at the front of the input queue prevents other packets in the same queue from being transferred through the switch fabric, even if their respective output ports are free. This happens because the packet at the front of the queue is destined for an output port that is currently busy or congested, blocking subsequent packets from moving forwards. 


### R12. 

YES, routers have multiple IP addresses. The number of IP addresses a router has depends on the number of interfaces or ports it has. 


### R13. 

The 32-bit binary equivalent of the IP address 223.1.3.27 is 11011111 00000001 00000011 00011011.


### R14.

#### An example of host Information:
- IP Address: 192.168.129.209
- Subnet Mask: 255.255.255.0
- Default Router: 192.168.129.234
- DNS Server: 192.168.129.234


### R15. 

An IP datagram sent from a source host to a destination host through 3 routers will travel over **eight interfaces** in total. Here's the detailed breakdown: 

1. **Source to Router 1:** 
    - Interface on the Source Host (sending)
    - Interface on Router 1 (receiving)
2. **Router 1 to Router 2:** 
    - Interface on Router 1 (sending)
    - Interface on Router 2 (receiving)
3. **Router 2 to Router 3:** 
    - Interface on Router 2 (sending)
    - Interface on Router 3 (receiving)
4. **Router 3 to Destination:**
    - Interface on Router 3 (sending)
    - Interface on the Destination Host (receiving)

**Forwarding Tables:** 
- Each router will index its forwarding table once to determine the next hop for the datagram. 
Therefore, **three forwarding tables** will be indexed to move the datagram from the source to the destination. 


### R18.

The five PCs at home obtain their IP addresses through the wireless **router's built-in DHCP server**, which assigns private IP addresses from a reserved range (e.g., 192.168.0.0/24). 

**YES, the wireless router uses NAT**. This is because NAT translates the private IP addresses of the five PCs to a single public IP address assigned by the ISP which helps not only in conserve the limited pool of IPv4 addresses, but also provide a layer of security by hiding the internal network structure. 


## Problems 

### P13. 

Subnet 1: 223.1.17.0/26 -> 223.1.17.0 - 223.1.17.63 (64 addresses)
Subnet 2: 223.1.17.64/25 -> 223.1.17.64 - 223.1.17.191 (128 addresses)
Subnet 3: 223.1.17.192/28 -> 223.1.17.192 - 223.1.17.207 (16 addresses)


### P16. 

For a subnet with prefix 128.119.40.128/26, any IP addresses in the range from 128.119.40.128 - 128.119.40.191 can be assigned to this network. 

The four subnets from the ISP block of addresses 128.119.40.64/26 are: 
1. 128.119.40.64/28 
2. 128.119.40.80/28 
3. 128.119.40.96/28 
4. 128.119.40.112/28


### P17.

![Figure 4.17](Computer-Networking-A-Top-Down-Approach-solutions/utils/4.17.png)

#### a. Network Addresses
- **Subnet A**: 214.97.254.0/24 -> 214.97.254.0 - 214.97.254.255 (256 addresses)
- **Subnet B**: 214.97.255.0/25 -> 214.97.255.0 - 214.97.255.127 (128 addresses)
- **Subnet C**: 214.97.255.128/25 -> 214.97.255.128 - 214.97.255.255 (128 addresses)
- **Subnet D**: 214.97.254.0/30 -> 214.97.254.0 - 214.97.254.3 (4 addresses)
- **Subnet E**: 214.97.254.4/30 -> 214.97.254.4 - 214.97.254.7 (4 addresses)
- **Subnet F**: 214.97.254.8/30 -> 214.97.254.8 - 214.97.254.11 (4 addresses)

#### b. Forwarding Tables

**Router 1**:

| **Longest Prefix Match**              | **Outgoing Interface** |
|---------------------------------------|------------------------|
| 11010110 01100001 11111110            | Subnet A              |
| 11010110 01100001 11111110 000000     | Subnet D              |
| 11010110 01100001 11111110 00001      | Subnet F              |

**Router 2**:

| **Longest Prefix Match**              | **Outgoing Interface** |
|---------------------------------------|------------------------|
| 11010110 01100001 11111111            | Subnet C              |
| 11010110 01100001 11111110 00001      | Subnet F              |
| 11010110 01100001 11111110 00000      | Subnet E              |

**Router 3**:

| **Longest Prefix Match**              | **Outgoing Interface** |
|---------------------------------------|------------------------|
| 11010110 01100001 11111110 000000     | Subnet D              |
| 11010110 01100001 11111110 00000      | Subnet E              |
| 11010110 01100001 11111111            | Subnet B              |
