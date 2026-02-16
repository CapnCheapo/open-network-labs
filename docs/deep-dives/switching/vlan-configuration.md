Virtual Local Area Networks, or VLANs, allow a switch to be carved up into separate little switches, allowing hosts assigned the
same VLAN number to communicate with each other, but not hosts in other VLANs. As discussed in a previous lesson, for devices in
separate networks to speak to each other a router is needed. Modern "layer 3" switches can accomplish this with minimal extra 
configuration. The alternative is to place one or more routers in between these VLANs. 

There was a note mentioning this lab can technically be considered complete without changing a single line of configuration.
Early in your networking studies, it is common to believe that a single VLAN corresponds to a single IP network. This doesn't
actually have to be the case. We will see later that a multilayer switch can be configured to route more than 1 subnet in a VLAN.
Depending on the situation, this might not be a good design. In what we call a `green field` deployment, it would make the most
sense to associate 1 subnet with 1 VLAN. In reality, networks outgrow their originally planned routing, subnets get migrated and
combined, and there are tools that allow these hosts to coexist on the same VLAN. 

Since our hosts do not have a default gateway assigned, they have no way to reach the other hosts, whether they are on a separate
VLAN or not. There are ways that the other hosts can be "sniffed out" in this VLAN based on their ARP traffic, but this kind of 
setup should never be used to keep hosts from communicating with each other in the same VLAN.

Why did we move the hosts out of VLAN 1? Could we have created only 2 VLANs, and left VLAN 1 (the default) as one of the department
VLANs? Absolutely. This is considered a best practice from a security standpoint. If the switch is not going to be connected to 
any other network device and you just want the devices to communicate out of the box, the switch will do that fine with VLAN 1. 
In a proper network environment though, where you have switches uplinked to other switches, VLAN 1 should be left alone. When you
learn about native VLANs and other switch services, you will discover that VLAN 1 is the default VLAN several important protocols
use to communicate via switches. For now, just understand that in most corporate networks you will not see devices connected to 
VLAN 1.


