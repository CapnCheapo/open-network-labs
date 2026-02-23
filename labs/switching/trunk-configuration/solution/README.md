# Trunk Configuration 
## Solution
Configure eth4 on both switches to be a trunk port.

## Walk-Through
1. Hosts cannot ping their mate.
```
accounting1:~$ ping 10.10.104.102
PING 10.10.104.102 (10.10.104.102) 56(84) bytes of data.
^C
--- 10.10.104.102 ping statistics ---
2 packets transmitted, 0 received, 100% packet loss, time 1056ms

marketing1:~$ ping 10.10.103.102
PING 10.10.103.102 (10.10.103.102) 56(84) bytes of data.
^C
--- 10.10.103.102 ping statistics ---
2 packets transmitted, 0 received, 100% packet loss, time 1042ms

sales1:~$ ping 10.10.102.102
PING 10.10.102.102 (10.10.102.102) 56(84) bytes of data.
^C
--- 10.10.102.102 ping statistics ---
1 packets transmitted, 0 received, 100% packet loss, time 0ms
```

2. Eth4 is setup with the default configuration (access port).
```
sw1#sh run int eth4
interface Ethernet4
sw1#sh run all int eth4 | i switchport mode
   switchport mode access
sw2#sh run all int eth4 | i switchport mode
   switchport mode access
```

3. Configure eth4 as a trunkport on both switches.
```
sw1#conf t
sw1(config)#int eth4
sw1(config-if-Et4)#switchport mode trunk 

sw2#conf t
sw2(config)#int eth4
sw2(config-if-Et4)#switchport mode trunk
```

4. Verify trunks have formed on both sides.
```
sw1#sh int eth4 trunk
Port            Mode            Status          Native vlan
Et4             trunk           trunking        1

Port            Vlans allowed
Et4             All

Port            Vlans allowed and active in management domain
Et4             1-4

Port            Vlans in spanning tree forwarding state
Et4             1-4

sw2#sh int eth4 trunk
Port            Mode            Status          Native vlan
Et4             trunk           trunking        1

Port            Vlans allowed
Et4             All

Port            Vlans allowed and active in management domain
Et4             1-4

Port            Vlans in spanning tree forwarding state
Et4             1-4
```

5. Verify each host can ping its mate.
```
accounting1:~$ ping 10.10.104.102
PING 10.10.104.102 (10.10.104.102) 56(84) bytes of data.
64 bytes from 10.10.104.102: icmp_seq=1 ttl=64 time=2.25 ms
64 bytes from 10.10.104.102: icmp_seq=2 ttl=64 time=1.31 ms

marketing1:~$ ping 10.10.103.102
PING 10.10.103.102 (10.10.103.102) 56(84) bytes of data.
64 bytes from 10.10.103.102: icmp_seq=1 ttl=64 time=2.29 ms
64 bytes from 10.10.103.102: icmp_seq=2 ttl=64 time=1.24 ms

sales1:~$ ping 10.10.102.102
PING 10.10.102.102 (10.10.102.102) 56(84) bytes of data.
64 bytes from 10.10.102.102: icmp_seq=1 ttl=64 time=1.79 ms
64 bytes from 10.10.102.102: icmp_seq=2 ttl=64 time=1.06 ms
```
