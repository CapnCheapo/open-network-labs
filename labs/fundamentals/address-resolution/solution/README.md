# Address Resolution
## Solution
The switch does not need an IP address for pc1, pc2, and pc3 to communicate with each other.

## Walk-Through
1. Sw1 is unable to ping pc1, pc2, or pc3.
```
sw1>en
sw1#ping 192.168.1.1
PING 192.168.1.1 (192.168.1.1) 72(100) bytes of data.

--- 192.168.1.1 ping statistics ---
5 packets transmitted, 0 received, 100% packet loss, time 40ms

sw1#ping 192.168.1.2
PING 192.168.1.2 (192.168.1.2) 72(100) bytes of data.

--- 192.168.1.2 ping statistics ---
5 packets transmitted, 0 received, 100% packet loss, time 40ms

sw1#ping 192.168.1.3 
PING 192.168.1.3 (192.168.1.3) 72(100) bytes of data.

--- 192.168.1.3 ping statistics ---
5 packets transmitted, 0 received, 100% packet loss, time 40ms
```

2. Pc1 is able to ping pc2 and pc3.
```
pc1:~$ ping 192.168.1.2
PING 192.168.1.2 (192.168.1.2) 56(84) bytes of data.
64 bytes from 192.168.1.2: icmp_seq=1 ttl=64 time=1.10 ms
64 bytes from 192.168.1.2: icmp_seq=2 ttl=64 time=0.574 ms
^C
--- 192.168.1.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1003ms
rtt min/avg/max/mdev = 0.574/0.837/1.100/0.263 ms
pc1:~$ ping 192.168.1.3
PING 192.168.1.3 (192.168.1.3) 56(84) bytes of data.
64 bytes from 192.168.1.3: icmp_seq=1 ttl=64 time=0.949 ms
64 bytes from 192.168.1.3: icmp_seq=2 ttl=64 time=0.634 ms
64 bytes from 192.168.1.3: icmp_seq=3 ttl=64 time=1.08 ms
^C
--- 192.168.1.3 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2037ms
rtt min/avg/max/mdev = 0.634/0.888/1.082/0.187 ms
```

3. Pc1 has used ARP to translate IP addresses into Layer 2 (MAC) addresses.
```
pc1:~$ ping 192.168.1.2
PING 192.168.1.2 (192.168.1.2) 56(84) bytes of data.
64 bytes from 192.168.1.2: icmp_seq=1 ttl=64 time=0.628 ms
^C
--- 192.168.1.2 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.628/0.628/0.628/0.000 ms
pc1:~$ ping 192.168.1.3
PING 192.168.1.3 (192.168.1.3) 56(84) bytes of data.
64 bytes from 192.168.1.3: icmp_seq=1 ttl=64 time=0.918 ms
64 bytes from 192.168.1.3: icmp_seq=2 ttl=64 time=0.664 ms
^C
--- 192.168.1.3 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1045ms
rtt min/avg/max/mdev = 0.664/0.791/0.918/0.127 ms
pc1:~$ ip neigh
192.168.1.3 dev eth1 lladdr aa:c1:ab:c6:f8:8a REACHABLE 
192.168.1.2 dev eth1 lladdr aa:c1:ab:bd:d7:41 REACHABLE 
```

4. Here is what the request looks like from pc2's perspective. Pc1 broadcasts an ARP request to ask who is pc2, pc2 responds back to
pc1 with its MAC address.
```
pc2:~$ sudo tcpdump -i eth1 arp
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth1, link-type EN10MB (Ethernet), snapshot length 262144 bytes
19:41:09.774850 ARP, Request who-has 192.168.1.2 tell 192.168.1.1, length 28
19:41:09.774858 ARP, Reply 192.168.1.2 is-at aa:c1:ab:bd:d7:41 (oui Unknown), length 28
```

5. Sw1 learns the MAC addresses for each host and associates a port number with each MAC address.
```
sw1#show mac address-table 
          Mac Address Table
------------------------------------------------------------------

Vlan    Mac Address       Type        Ports      Moves   Last Move
----    -----------       ----        -----      -----   ---------
   1    aac1.ab0d.c452    DYNAMIC     Et2        1       0:03:07 ago
   1    aac1.ab22.3d56    DYNAMIC     Et3        1       0:03:03 ago
   1    aac1.abaf.7a83    DYNAMIC     Et1        1       0:03:07 ago
Total Mac Addresses for this criterion: 3
```

### Deep-Dive
See (https://github.com/CapnCheapo/open-network-labs/tree/main/docs/deep-dives/fundamentals-address-resolution.md)

## Next Steps

Based on this lab, you might want to explore:

- **[This Lab]** – This lab
- **[That Lab]** – This other lab

For a guided sequence, see:
- `docs/learning-paths/fundamentals-linear.md`
