# Basic L2 Connectivity
## Solution
Ports Et1 and Et2 were in a shutdown state.

## Walk-Through

1. pc1 can't ping pc2.
```
pc1:~$ ping 192.168.1.2
PING 192.168.1.2 (192.168.1.2) 56(84) bytes of data.
^C
--- 192.168.1.2 ping statistics ---
9 packets transmitted, 0 received, 100% packet loss, time 8204ms
```

2. pc2 can't ping pc1.
```
pc2:~$ ping 192.168.1.1
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
^C
--- 192.168.1.1 ping statistics ---
3 packets transmitted, 0 received, 100% packet loss, time 2040ms
```

3. Switch shows interfaces Et1 and Et2 in status disabled.
```
sw1>en
sw1#show interface status
Port       Name   Status       Vlan     Duplex Speed  Type            Flags Encapsulation
Et1               disabled     1        full   1G     EbraTestPhyPort                   
Et2               disabled     1        full   1G     EbraTestPhyPort                   
Ma0               connected    routed   a-full a-1G   10/100/1000
```

4. Switchports are enabled.
```
sw1#conf t
sw1(config)#interface Et1
sw1(config-if-Et1)#no shutdown
sw1(config-if-Et1)#interface Et2
sw1(config-if-Et2)#no shutdown
```

5. Configuration mode is exited and port status checked again.
```
sw1(config-if-Et2)#end
sw1#show interface status
Port       Name   Status       Vlan     Duplex Speed  Type            Flags Encapsulation
Et1               connected    1        full   1G     EbraTestPhyPort                   
Et2               connected    1        full   1G     EbraTestPhyPort                   
Ma0               connected    routed   a-full a-1G   10/100/1000                       
```

6. pc1 can now ping pc2
```
pc1:~$ ping 192.168.1.2
PING 192.168.1.2 (192.168.1.2) 56(84) bytes of data.
64 bytes from 192.168.1.2: icmp_seq=1 ttl=64 time=1.05 ms
64 bytes from 192.168.1.2: icmp_seq=2 ttl=64 time=0.699 ms
^C
--- 192.168.1.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1005ms
rtt min/avg/max/mdev = 0.699/0.872/1.045/0.173 ms
```

7. pc2 can now ping pc1
```
pc2:~$ ping 192.168.1.1
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=0.716 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=0.601 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=64 time=0.598 ms
^C
--- 192.168.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2064ms
rtt min/avg/max/mdev = 0.598/0.638/0.716/0.054 ms
```

## Deep-Dive
See (https://github.com/CapnCheapo/open-network-labs/tree/main/docs/deep-dives/fundamentals/basic-l2-connectivity.md)

## Next Steps

Based on this lab, you might want to explore:

- **[This Lab]** – This lab
- **[That Lab]** – This other lab

For a guided sequence, see:
- `docs/learning-paths/fundamentals-linear.md`
