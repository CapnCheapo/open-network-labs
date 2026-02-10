Up until now, we have not really discussed the layers involved with communicating over the network. Mostly because a complete knowledge
of them is not necessary to dive in with basic troubleshooting and configuration tasks. However, to truly understand why things work
the way they do, it's helpful to discuss some layering. We will not discuss all of them in this deep-dive, but rather the ones you are
likely to hear about early in your networking career.

| # | Layer Name  | Basic Description                        |
| - | ----------- | ---------------------------------------- |
| 1 | Physical    | Cabling, connectors, voltage             |
| 2 | Data Link   | Physical addressing, frame transmission  |
| 3 | Network     | Logical addressing and routing           |
| 7 | Application | Network protocols like SSH and HTTP      |

Routers are primarily concerned with layer 3, but all network devices are involved with other layers. Layer 3 involves IP addressing and
routing. We say "logical addressing" because it represents an address that represents you from the source of your packet's life to its
destination (with some exceptions, of course, but you knew I would say that!) 

Switches are mostly involved with layer 2, although many switches today can also function as routers. We call these `layer 3 switches` 
and that is what is connected to this lab by default. Many businesses choose to implement entirely layer 2 and layer 3 switches because
of cost savings, fewer devices needing to be deployed, and generally easier troubleshooting. Layer 3 switches are not as feature-rich as
many routers, but they handle the features that most small and medium-sized businesses require. 

What do we mean about logical addressing though? Let's find the MAC address of pc1:

```
pc1:~$ ip addr show dev eth1
179: eth1@if178: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9500 qdisc noqueue state UP group default 
    link/ether **aa:c1:ab:95:7f:79** brd ff:ff:ff:ff:ff:ff link-netnsid 1
    inet 192.168.1.1/24 scope global eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a8c1:abff:fe95:7f79/64 scope link proto kernel_ll 
       valid_lft forever preferred_lft forever
```

The section marked with asterisks is the MAC address for this interface. You might also hear this called the link local address, or
the layer 2 address. This is called a **burned in address** or BIA. Unless the manufacturer makes a mistake (and this does happen
from time to time!) or under special circumstances, no two devices will have the same MAC address. The first half, in this case aa.c1.ab
is called an OUI or organizational unique identifier. They are assigned to companies and can actually be used to identify the maker 
(and sometimes type) of the device that is connected. This is sometimes helpful when trying to identify a "mystery device" on the network.
The remaining half is assigned by the manufacturer and is supposed to be unique. 

It is common for networking students to ask, "If every device on a network already has this unique burned-in address, why bother with 
IP addresses at all? It just seems like extra work." It's a nice idea at first thought, but the reality is there are BILLIONS of devices
with MAC addresses out there, and there can be about 70 trillion total. Manufacturers ship their devices all over the world. For devices
to route by MAC address, somebody would have to keep a record of all these billions of MAC addresses and how they can be reached. How do 
we update this record when a device moves? Who controls the record? It's simply not scalable.

The magic behind packets traversing the millions of paths across the internet is possible due to 2 main principles. First, there is no 
centralized list- networks are responsible for letting the internet know which networks are accessible through their infrastructure, and
second- due to subnetting and block summarization we don't have to advertise all 4.3 billion IP addresses individually. We can group them
by subnet or even do something called supernetting, where a provider may say "I own everything that starts with 120. so i'm going to
advertise 120.0.0.0/8, you send me your traffic, and I'll figure out the details."

With the exception of devices like firewalls that can change your IP address for a variety of reasons, your IP address will stay the 
same from source to destination. Your packet's MAC address changes as it crosses different media. Ethernet is considered to be one type
of network medium. When we connected these 3 PCs to a switch and left the switch configuration as default, we created an Ethernet network
among them. Wifi is another layer 2 medium. There are older media that exist that you may run across, but these are the basics. Even 
when two routers are connected to each other, they typically form a small network we call a point-to-point or P2P network, complete with
MAC addresses. When your packet goes through its final router hop, the destination router is going to attach a MAC address and place the
packet on the local ethernet, where the resolution process will help it find the final destination host. It is very important that this
concept is understood early on, because the most of network engineering is built on top of these principles.

By the way, each layer encapsulates the layers below them in some way or another. Layer 3 PDUs (protocol data units) are called packets
and encapsulate everything (layer 3-7) underneath. The Layer 2 PDU is actually called a frame, although you will often hear the term
"packet" used in a generic sense. The layer 2 frame consists of the source and destination MAC addresses of the local network. 

All of this is to establish a point. Routers deal with IP addresses and layer 3 packets. Switches deal with layer 2 frames. If a switch 
is just acting like a regular old switch and not a layer 3 switch, it is not able to directly able to "talk" to other devices on the
network. So what's the point, then? To understand completely, we would have to discuss the topic of switches versus hubs. Hubs are 
basically dead technology at this point, largely replaced by switches which perform layer 2 transmission faster and more efficiently. 

Switches learn MAC addresses by spying on traffic that goes by. When a switch associates a MAC address with a port, it is able to 
get the traffic to its destination faster. Otherwise, a switch has to act like a hub and flood the traffic out of all ports except the 
source, hoping that somebody will respond. There are other benefits to switches, but this is enough information at this point of your
journey. 

So how do we figure out the destination device's MAC address if we don't specify it? There's a protocol for that! ARP, or Address
Resolution Protocol allows a host to broadcast on a medium like ethernet (framing the traffic with ff:ff:ff:ff:ff:ff) which allows
the traffic to be seen by every device on an ethernet network. Inside this ARP packet will be a request that asks the following 
question, "Hey everybody. I am trying to reach 192.168.1.2. If that's you, tell me your MAC address." Every device will see this,
but under normal circumstances only the destination host will respond. The response will be something like "Hey source host, my 
MAC address is aa:c1:ab:95:7f:80." On the way back, the switch learns this host's MAC address and places it in the MAC address table.
The source host now knows pc2's MAC address and it crafts a frame with its source MAC and the destination's MAC, and off the traffic
goes! 

The host has what's called an ARP table, this creates a triplet association: MAC address, IP address, and outgoing interface. At that
point, the host can query its own ARP table when it needs to have future communication with this host, without having to go through
the ARP query all over again. The entries in this table do eventually time out, so if two hosts go a long time without talking to 
each other, it may be necessary for the host to ARP again. If the hosts had to do this every time it would slow down the network
quite a bit, because other hosts have to stop what they're doing and check if this broadcast pertains to them. An ARP query every 
once in a while is not a huge problem because in modern networks this process completes in a matter of milliseconds. You may notice
when pinging a host from a Cisco IOS switch, the first ping may drop, but the rest go through, and subsequent pings have no drops-
this is usually the device having to ARP for a connection that has timed out from the table.

Do not confuse the process hosts use to find MAC addresses with the process switches use to learn MAC addresses. Switches store
SOURCE addresses as it sees them cross a port. The switch builds a MAC address table which is (for all intents and purposes) a tuple
of source port and MAC address. Whereas the hosts populate an ARP table based on the destination IP and MAC address, plus source port
as a triplet. 

The topics in this document are critical to understand before we add complexity on top of the operation. However, there are some 
practical "tricks" that can be used to check on the health and population of a network. For example, a network engineer can run
a "ping sweep" across a subnet (for example, quickly ping all addresses in 192.168.1.0/24) and the ARP table can be checked to get
a count of about how many devices are on the network. The MAC address table can be checked for similar reasons. If a port is up but
there is no traffic crossing, the switch may not have a MAC address for the device and it may be having problems (or it's just
not very "chatty", they pay us the big bucks to make the final call on which it is!)

## Suggested Resources
- TBD
