# Host Identity 
## Solution
pc1 needed an IP address and netmask assignment out of the 192.168.50.0/24 subnet.

## Walk-Through

1. The interface configuration is inspected on pc2.
```
pc2:~$ ip address show dev eth1
57: eth1@if56: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9500 qdisc noqueue state UP group default 
    link/ether aa:c1:ab:68:94:d6 brd ff:ff:ff:ff:ff:ff link-netnsid 1
    inet 192.168.50.50/24 scope global eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a8c1:abff:fe68:94d6/64 scope link proto kernel_ll 
       valid_lft forever preferred_lft forever
```

2. pc1 can be assigned any address in 192.168.60.x other than .0, .50, or greater than .254.
```
pc1:~$ sudo ip address add 182.168.50.1/24 dev eth1
pc1:~$ ip address show dev eth1
61: eth1@if62: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9500 qdisc noqueue state UP group default 
    link/ether aa:c1:ab:81:4b:6a brd ff:ff:ff:ff:ff:ff link-netnsid 1
    inet 192.168.50.1/24 scope global eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a8c1:abff:fe81:4b6a/64 scope link proto kernel_ll 
       valid_lft forever preferred_lft forever
```

3. pc1 can ping pc2.
```
pc1:~$ ping 192.168.50.50
PING 192.168.50.50 (192.168.50.50) 56(84) bytes of data.
64 bytes from 192.168.50.50: icmp_seq=1 ttl=64 time=1.12 ms
64 bytes from 192.168.50.50: icmp_seq=2 ttl=64 time=0.675 ms
^C
--- 192.168.50.50 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1005ms
rtt min/avg/max/mdev = 0.675/0.898/1.122/0.223 ms
```

4. pc3 is located in subnet 192.168.123.0/24.
```
pc3:~$ ip address show eth1
60: eth1@if59: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9500 qdisc noqueue state UP group default 
    link/ether aa:c1:ab:72:8f:8e brd ff:ff:ff:ff:ff:ff link-netnsid 1
    inet 192.168.123.100/24 scope global eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a8c1:abff:fe72:8f8e/64 scope link proto kernel_ll 
       valid_lft forever preferred_lft forever1
```

5. pc1 is not able to ping 192.168.123.100.
```
pc1:~$ ping 192.168.123.100
ping: connect: Network unreachable
```

## Deep-Dive
See (https://github.com/CapnCheapo/open-network-labs/tree/main/docs/deep-dives/fundamentals/host-identity.md)

## Next Steps

Based on this lab, you might want to explore:

- **[This Lab]** – This lab
- **[That Lab]** – This other lab

For a guided sequence, see:
- `docs/learning-paths/fundamentals-linear.md`
