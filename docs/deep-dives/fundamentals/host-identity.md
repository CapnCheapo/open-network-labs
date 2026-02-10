Two of the most important concepts for network professionals to know inside-and-out are IP addressing and subnetting. We are only
scratching the surface of these topics in this lab, but they are a critical starting point. In the basic-l2-connectivity lab, we
learned that hosts must have an IP address to communicate with other devices on a network. This lab expands on that to include both 
an IP address AND a subnet mask (netmask). This combination together makes up the host's identity.

We already know that an IP address can be thought of as your mailing address (for example, 123 Elm St.) You might loosely look at 
the netmask as the city and state (Roswell, NM). If we address a letter to 200 Elm St., Roswell, NM, we would expect that our letter
would be processed by our local post office only. However, if this letter is addressed to 100 Main St., Chicago, IL, we would expect
our letter to be transported by truck with other regional letters and handled by local and regional mail facilities. 

Think of the IP address and netmask combination as "who am I?" and "what is local to me?" The host uses this information to decide
the first steps for the direction packets of data will travel over the network. It's common for network younglings to assume the 
network device the host is connected to has a big list of everything the host could possibly talk to, and just "handles it". This
is definitely not the case. In fact, if we wanted to, we could directly connect pc1 and pc2 to each other, assign IP addresses and
netmasks, and these two hosts would be able to communicate without the use of a switch or router sitting between them.

Subnetting is a much deeper topic than what is covered in this lab, but there is a cheat code to help you get started. When we
connected to pc2 we saw it had an address of 192.168.50.50/24. At the simplest level, this tells us that the host has an IP address
of 192.168.50.50 and the /24 allows us to break this address up nice and even. The network this host is in is baked into the address, 
and the netmask is the key to knowing which part is the network and which part is the host. /24 is easy because it means the first
3 octets of the address are the network, and the last octet is the host. For pc2 this means the network is 192.168.50 and the host is
50. This network can have 254 hosts in it: 192.168.50.1 through 192.168.50.254. 0 and 255 are reserved and you'll learn about them
later. 

So returning to pc1, we can pick any address other than 192.168.50.0, 192.168.50.255, or 192.168.50.50 (we can't give two hosts 
the same IP address, otherwise how will we differentiate the two?) Once the IP and netmask are assigned to pc1, it has enough 
information to decide what process to take to speak to other devices. If the device we are trying to reach has an address that 
starts with 192.168.50., we can communicate with them directly over the network. For right now, you can view the switch as a 
device that allows multiple devices ON THE SAME NETWORK to reach each other without having to run a web of network cables between
all of them (it's easy to connect 2 devices together, but how would you allow 3 devices to talk? 150 devices?)

So how does pc3 play into all of this? PC3 has an address of 192.168.123.100/24 -- that's in Chicago and we're in Anchorage!
With a /24 netmask, the first 3 octets have to match EXACTLY for these two hosts to communicate. 192.168. is fine but .50 and
.123 do not. These hosts can't communicate as-is because they are not in the same network. Can we take steps to make them
communicate? Absolutely, but you'll have to wait for future lessons! Even if we connected pc1 and pc3 directly to each other,
they are going to act like "ships passing in the night" and will never be able to talk to each other without additional 
configuration.

/24 was picked for this lab because it's an "easy" subnet. There's a good chance your home's wifi network is using a /24 subnet. 
As a matter of fact, there's even a good chance it is using a network starting with 192.168. This is what we call a private
address block, meaning it is not routable over the internet. Private and public addressing are topics we will get into later,
as are subnets that are not /24. As a network engineer, you will see a variety of masks in the wild- /26, /18, /8, /31. Each
of these separates the network portion from the host portion in a different way. 

For the purposes of this lab, we have intentionally blocked passage through a rabbit hole that you'll need to travel down 
eventually. /24 is not just a random number chosen out of the air to tell you the first 3 octets are the network address.
It actually signifies that 24 bits of a 32 bit IP address belong to the network. Sometimes (for example, on an IOS switch) 
you will see /24 written as 255.255.255.0. These two "things" are the same. Dealing with IP addresses and netmasks is actually
an exercise in binary math. 1's and 0's. The language under your computer's hood. To be somebody with the word network in his
or her job title, you should reach a point where you can be given an IP address and netmask, you can tell what **class* of 
network this is (a topic we haven't discussed yet), and what the first and last usable addresses are in the block, in your head
(or at least with a pencil and paper).

From a practical standpoint, you may be called in to troubleshoot why 2 hosts that are "supposed to be on the same network" can't 
communicate. Fun fact, if you are using a /25 netmask, hosts 192.168.50.126 and 192.168.50.129 are not on the same network! 
When dealing with "easy" netmasks like /8, /16, and /24 these sorts of problems rarely come up, but when you start dividing 
things up beyond the octet boundary, it's a common mistake for somebody to get the math wrong on the netmask calculation and
introduce subtle accessibility problems. 

## Suggested Resources
- TBD
