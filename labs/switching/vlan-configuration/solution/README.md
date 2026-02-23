# VLAN Configuration 
## Solution
Configure eth4 as a trunk port on both switches.

## Walk-Through
1. Hosts are not able to ping their mate.
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

2. Eth4 is in the default configuration (access port).
```
sw1#sh run int eth4
interface Ethernet4
sw1#sh run all int eth4 | i switchport mode
   switchport mode access

```
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
