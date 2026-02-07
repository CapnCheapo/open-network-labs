# Default Gateway
## Solution
The hosts were missing the default gateway configuration. As a result, traffic destined for non-local networks had no next hop and was never forwarded off the local subnet.

## Walk-Through

1. pc1 can ping pc2.
```
pc1:~$ ping 192.168.1.2
PING 192.168.1.2 (192.168.1.2) 56(84) bytes of data.
64 bytes from 192.168.1.2: icmp_seq=1 ttl=64 time=0.676 ms
64 bytes from 192.168.1.2: icmp_seq=2 ttl=64 time=0.564 ms
^C
--- 192.168.1.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1006ms
```

2. pc2 can ping pc1. Local network connectivity is confirmed.
```
pc2:~$ ping 192.168.1.1
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=0.689 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=0.544 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=64 time=0.619 ms
^C
--- 192.168.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2036ms
rtt min/avg/max/mdev = 0.544/0.617/0.689/0.059 ms
```

3. pc1 can't ping 1.1.1.1.
```
pc1:~$ ping 1.1.1.1
ping: connect: Network unreachable
```

4. pc2 can't ping 1.1.1.1.
```
pc2:~$ ping 1.1.1.1
ping: connect: Network unreachable
```

5. Routing table on pc1 is checked. Only local networks are shown.
```
pc1:~$ ip route
172.20.20.0/24 dev eth0 proto kernel scope link src 172.20.20.4 
192.168.1.0/24 dev eth1 proto kernel scope link src 192.168.1.1
```

6. Default gateway is added on pc1.
```
pc1:~$ sudo ip route add default via 192.168.1.100 dev eth1
```

7. Routing table is checked again. A default gateway of 192.168.1.100 is now shown.
```
pc1:~$ ip route
default via 192.168.1.100 dev eth1 
172.20.20.0/24 dev eth0 proto kernel scope link src 172.20.20.4 
192.168.1.0/24 dev eth1 proto kernel scope link src 192.168.1.1 
```

8. pc1 can now ping 1.1.1.1.
```
pc1:~$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=64 time=1.28 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=64 time=0.737 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=64 time=0.762 ms
^C
--- 1.1.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2010ms
rtt min/avg/max/mdev = 0.737/0.924/1.275/0.247 ms
```

9. Routing table on pc2 is checked. Only local networks are shown.
```
pc2:~$ ip route
172.20.20.0/24 dev eth0 proto kernel scope link src 172.20.20.3 
192.168.1.0/24 dev eth1 proto kernel scope link src 192.168.1.2
```

10. Default gateway is added on pc2.
```
pc2:~$ sudo ip route add default via 192.168.1.100 dev eth1
```

11. Routing table is checked again.
```
pc2:~$ ip route
default via 192.168.1.100 dev eth1 
172.20.20.0/24 dev eth0 proto kernel scope link src 172.20.20.3 
192.168.1.0/24 dev eth1 proto kernel scope link src 192.168.1.2 
```

12. pc2 can now ping 1.1.1.1.
```
```
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=64 time=1.32 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=64 time=0.916 ms
^C
--- 1.1.1.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1004ms
rtt min/avg/max/mdev = 0.916/1.120/1.324/0.204 ms
```

## Deep-Dive
See (https://github.com/CapnCheapo/open-network-labs/tree/main/docs/deep-dives/fundamentals/default-gateway.md)

## Next Steps

Based on this lab, you might want to explore:

- **[This Lab]** – This lab
- **[That Lab]** – This other lab

For a guided sequence, see:
- `docs/learning-paths/fundamentals-linear.md`
