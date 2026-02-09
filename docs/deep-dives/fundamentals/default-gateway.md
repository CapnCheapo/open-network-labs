In the host identity lab, we cover how the netmask helps separate the network and host portions of an IP address, and we
allowed two hosts on the same network to communicate with each other. Well, what happens when they are NOT on the same 
network and they need to communicate with each other?

To return to the post office analogy, pc1 is located at 123 Mockingbird Ln, Roswell, NM. pc2 is located at 1500 Pennsylvania Ave, 
Roswell, NM. The message sent from pc1 to pc2 is going to stay in our local post office. How do we reach 1.1.1.1 which is in 
New York City though? Since it is not on the 192.168.1.0/24 network we don't exactly know what to do with it. Do we just tell pc1 
"find an efficient path between me and this other host out there at 1.1.1.1"? Not likely. Just as you don't call up your local post 
office in Roswell and tell them how to get your letter to New York. You address and stamp your letter and trust that the post office
system will get it to New York in the most practicable way possible. 

In networking, the post office is considered to be the router. When the host doesn't know what to do with a packet, it addresses it to 
a router which is (we hope) connected on our local network. From there, this router may decide it knows exactly how to reach the other 
network, and it will send the packet there, or it may decide, "I don't know, either" and hand it off to it's own default gateway! 

How routers decide where to send packets destined for other networks can be, quite frankly, the subject of hundreds of labs and 
thousands of pages in a large number of books. At the most basic level, specifying the default gateway tells the host (or network
device) "if something is not on my local network, send it to this router and let it deal with the problem."

Notice in this lab, the first thing we do is have pc1 and pc2 ping each other. They have the addresses 192.168.1.1/24 and 192.168.1.2/24,
respectively. At this point, there is no default gateway set. The purpose of these initial pings is just to show that hosts can be 
connected in a local network and never need a default gateway. Only when the destination address is determined to be on another network
do we get routers involved. We have reached the most basic definition of a router: a device that allows devices in other networks to 
communicate with each other. 

We now check pc1's routing table to see if it knows about a default gateway by using the `ip route` command. In these labs, we always
ignore interface eth0-- that is how you are physically connecting to these labs, but in a real production network you may only see
one interface connected. In this case, both PCs have eth1 connected to a layer 3 switch, which is a switch that can also perform 
routing functions. The other item the routing table currently shows is what we call a connected route (specifically a local route, 
but for now you can consider them to be the same.) This route shows that we have an interface in the 192.168.1.0 network, eth1, and
it has an address of 192.168.1.1. You will always see entries in the routing table for directly connected networks. 

After the default gateway is added, if you look at the routing table again, you will see an additional line:
```
default via 192.168.1.100 dev eth1
```
This entry says, "If the destination is not on my local network, and I don't have an interface in the destination network, send it
to the router, which has an address of 192.168.1.100". On network devices, you are more likely to see a routing table entry of 
0.0.0.0/0 specifying the default route or "gateway of last resort." 

It just so happens, our router knows what to do with 1.1.1.1 because there is a routing table entry specifically for it! In fact,
1.1.1.1 is connected to what's called a loopback interface on the router. For now, just think of this as the router pretending it 
is a host with that address. It will respond to pings.

We can check the routing table on sw1 with the `show ip route` command. 

```
sw1#sh ip route

VRF: default
Source Codes:
       C - connected, S - static, K - kernel,
       O - OSPF, O IA - OSPF inter area, O E1 - OSPF external type 1,
       O E2 - OSPF external type 2, O N1 - OSPF NSSA external type 1,
       O N2 - OSPF NSSA external type2, O3 - OSPFv3,
       O3 IA - OSPFv3 inter area, O3 E1 - OSPFv3 external type 1,
       O3 E2 - OSPFv3 external type 2,
       O3 N1 - OSPFv3 NSSA external type 1,
       O3 N2 - OSPFv3 NSSA external type2, B - Other BGP Routes,
       B I - iBGP, B E - eBGP, R - RIP, I L1 - IS-IS level 1,
       I L2 - IS-IS level 2, A B - BGP Aggregate,
       A O - OSPF Summary, NG - Nexthop Group Static Route,
       V - VXLAN Control Service, M - Martian,
       DH - DHCP client installed default route,
       DP - Dynamic Policy Route, L - VRF Leaked,
       G  - gRIBI, RC - Route Cache Route,
       CL - CBF Leaked Route

Gateway of last resort is not reachable

 C        1.1.1.1/32
           directly connected, Loopback0
 C        192.168.1.0/24
           directly connected, Vlan1
```

Wow, that's a lot of information! Actually, it's not bad at all once you know what you're looking at. Jump straight to the bottom.
See the letters? For now, think of one letter as one route (not always the case, but just go with me on this.) Both of these routes
are `C` routes, or connected routes. Just like we saw on pc1, our router makes an entry for every network it is directly connected to.
It also shows we are directly connected to that myatery host 1.1.1.1, in fact, we see loopback0 which means this router is pretending
to be 1.1.1.1.

Would this router be able to hand the packet off to another router if it didn't know how to reach 1.1.1.1? Nope. There are no other
routing entries here, and there is no default gateway defined. If the connected route for 1.1.1.1 didn't exist, sw1 would drop the 
packet and let pc1 know that the destination network is unreachable. Here is what sw1 might look like if it did have its own default
gateway:

```
sw1#sh ip route

VRF: default
Source Codes:
       C - connected, S - static, K - kernel,
       O - OSPF, O IA - OSPF inter area, O E1 - OSPF external type 1,
       O E2 - OSPF external type 2, O N1 - OSPF NSSA external type 1,
       O N2 - OSPF NSSA external type2, O3 - OSPFv3,
       O3 IA - OSPFv3 inter area, O3 E1 - OSPFv3 external type 1,
       O3 E2 - OSPFv3 external type 2,
       O3 N1 - OSPFv3 NSSA external type 1,
       O3 N2 - OSPFv3 NSSA external type2, B - Other BGP Routes,
       B I - iBGP, B E - eBGP, R - RIP, I L1 - IS-IS level 1,
       I L2 - IS-IS level 2, A B - BGP Aggregate,
       A O - OSPF Summary, NG - Nexthop Group Static Route,
       V - VXLAN Control Service, M - Martian,
       DH - DHCP client installed default route,
       DP - Dynamic Policy Route, L - VRF Leaked,
       G  - gRIBI, RC - Route Cache Route,
       CL - CBF Leaked Route

Gateway of last resort:
 S        0.0.0.0/0 [1/0]
           via 192.168.2.2, Ethernet3

 C        1.1.1.1/32
           directly connected, Loopback0
 C        192.168.1.0/24
           directly connected, Vlan1
 C        192.168.2.0/24
           directly connected, Ethernet3
```

For the example above, we connected sw1 to a new device, sw2, and gave them addresses in the 192.168.2.0/24 network. Then we set
a `static route` (a topic to be covered later) pointing 0.0.0.0/0 to 192.168.2.2. The router also calls this the "gateway of last
resort". From a routing standpoint, certain routes are going to take priority over other routes (yet another subject for another lab!)
but if all else fails, we should send the packet to 192.168.2.2. From there, the router on the other end has a similar decision to make.
Do I know about this destination network already? Otherwise, do I have somewhere I can send this packet to if I am not sure? This kind 
of logic, in its most simplified sense, can get your packet from a host located at your desk in Roswell, to a host located in Siberia.

Troubleshooting the default gateway often comes down to a handful of checks. Is the default gateway set at all? Is it the correct 
address? Is the default gateway in the same subnet as your host? (There are some very specific advanced cases where a default gateway
is not in the same subnet as the host, but for now you can pretend this is a hard requirement.) Can I ping the default gateway? 

Sometimes you're not troubleshooting the source, but rather the destination. For a ping between 192.168.1.1 and 1.1.1.1, not only does
192.168.1.1 need to have an idea how to get the packets out to the router, but 1.1.1.1 needs to have a return path. If the destination
is under your administrative control, you will need to perform the same troubleshooting on the other end. This detail tends to throw
off junior network technicians. If the remote host and other routers in the path are not under your control, you may need to get external
parties involved so that end-to-end troubleshooting can be done, but always remember to check the hosts at both ends before assuming
there is a problem with a router or switch.

## Suggested Resources
- [Practical Networking -- Network Devices](https://www.youtube.com/watch?v=bj-Yfakjllc&list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi&index=1&pp=iAQB)
- [Practical Networking -- Subnetting Mastery](https://www.youtube.com/playlist?list=PLIFyRwBY_4bQUE4IB5c4VPRyDoLgOdExE)
- [Subnetting Practice](https://subnetipv4.com/)
- Cisco Press, *CCNA 200-301 Official Cert Guide*, Chapter 1
- O’Reilly, *Computer Networking: A Top-Down Approach*, Section 1.4
- RFC 1122 – Requirements for Internet Hosts
