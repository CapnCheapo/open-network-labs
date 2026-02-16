# VLAN Configuration 
## Solution
Create VLANs 2, 3, and 4. Assign each switchport to the appropriate VLAN.

## Walk-Through
1. Create VLANs through VLAN configuration mode, then assign ports.
```
sw1>en
sw1#conf t
sw1(config)#vlan 2
sw1(config-vlan-2)#name Sales
sw1(config-vlan-2)#vlan 3
sw1(config-vlan-3)#name Marketing
sw1(config-vlan-3)#vlan 4
sw1(config-vlan-4)#name Accounting
sw1(config-vlan-4)#exit
sw1(config)#int eth1-3
sw1(config-if-Et1-3)#switchport access vlan 2
sw1(config-if-Et1-3)#int eth4-5
sw1(config-if-Et4-5)#switchport access vlan 3
sw1(config-if-Et4-5)#int eth6-8
sw1(config-if-Et6-8)#switchport access vlan 4
sw1(config-if-Et6-8)#end
```

2. Verify the VLANs have been created and port assignment is correct.
```
sw1#show vlan brief
VLAN  Name                             Status    Ports
----- -------------------------------- --------- -------------------------------
1     default                          active    
2     Sales                            active    Et1, Et2, Et3
3     Marketing                        active    Et4, Et5
4     Accounting                       active    Et6, Et7, Et8
```

3. Verify sales1 can ping sales2 and sales3, but not any other host.
```
sales1:~$ ping 10.10.102.102
PING 10.10.102.102 (10.10.102.102) 56(84) bytes of data.
64 bytes from 10.10.102.102: icmp_seq=1 ttl=64 time=1.30 ms
64 bytes from 10.10.102.102: icmp_seq=2 ttl=64 time=0.647 ms
^C
--- 10.10.102.102 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1005ms
rtt min/avg/max/mdev = 0.647/0.974/1.301/0.327 ms
sales1:~$ ping 10.10.102.103
PING 10.10.102.103 (10.10.102.103) 56(84) bytes of data.
64 bytes from 10.10.102.103: icmp_seq=1 ttl=64 time=1.13 ms
64 bytes from 10.10.102.103: icmp_seq=2 ttl=64 time=0.602 ms
^C
--- 10.10.102.103 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1005ms
rtt min/avg/max/mdev = 0.602/0.867/1.132/0.265 ms
sales1:~$ ping 10.10.104.101
PING 10.10.104.101 (10.10.104.101) 56(84) bytes of data.
^C
--- 10.10.104.101 ping statistics ---
5 packets transmitted, 0 received, 100% packet loss, time 4109ms
```

4. Verify accounting1 can ping accounting2 and accounting3, but not any other host.
```
accounting1:~$ ping 10.10.104.102
PING 10.10.104.102 (10.10.104.102) 56(84) bytes of data.
64 bytes from 10.10.104.102: icmp_seq=1 ttl=64 time=1.00 ms
^C
--- 10.10.104.102 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 1.001/1.001/1.001/0.000 ms
accounting1:~$ ping 10.10.104.103
PING 10.10.104.103 (10.10.104.103) 56(84) bytes of data.
64 bytes from 10.10.104.103: icmp_seq=1 ttl=64 time=1.02 ms
64 bytes from 10.10.104.103: icmp_seq=2 ttl=64 time=0.624 ms
^C
--- 10.10.104.103 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1005ms
rtt min/avg/max/mdev = 0.624/0.821/1.018/0.197 ms
accounting1:~$ ping 10.10.102.101
PING 10.10.102.101 (10.10.102.101) 56(84) bytes of data.
^C
--- 10.10.102.101 ping statistics ---
4 packets transmitted, 0 received, 100% packet loss, time 3081ms
```

5. Verify marketing1 can ping marketing2, but not any other host.
```
marketing1:~$ ping 10.10.103.102
PING 10.10.103.102 (10.10.103.102) 56(84) bytes of data.
64 bytes from 10.10.103.102: icmp_seq=1 ttl=64 time=1.16 ms
64 bytes from 10.10.103.102: icmp_seq=2 ttl=64 time=0.646 ms
^C
--- 10.10.103.102 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1005ms
rtt min/avg/max/mdev = 0.646/0.902/1.158/0.256 ms
marketing1:~$ ping 10.10.104.101
PING 10.10.104.101 (10.10.104.101) 56(84) bytes of data.
^C
--- 10.10.104.101 ping statistics ---
3 packets transmitted, 0 received, 100% packet loss, time 2048ms
```
