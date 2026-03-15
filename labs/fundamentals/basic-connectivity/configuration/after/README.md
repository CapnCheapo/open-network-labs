# basic-connectivity
## Topology
```mermaid
graph LR
  lindapc(lindapc)
  bobpc(bobpc)

  lindapc --- bobpc

  class lindapc,bobpc host
```

## Solution
IP address 192.168.1.100/24 was assigned to lindapc and 192.168.1.101/24 to bobpc.

---

## Walk-Through

1. Log into bob's pc. For future labs, we will no longer show the login process.
```
 ssh lab@clab-basic-connectivity-bobpc
lab@clab-basic-connectivity-bobpc's password: 
bobpc:~$
```

2. Changing network interface configuration in linux requires root privileges, so start
the command with sudo. The `ip addr add` command can be used to add 192.168.1.100/24 to
the desired interface, in this case, eth1.
```
bobpc:~$ ip addr add 192.168.1.100/24 dev eth1
bobpc:~$ exit
```
We have one side of our configuration complete.

3. Now log into Linda's PC.
```
 ssh lab@clab-basic-connectivity-lindapc
lab@clab-basic-connectivity-lindapc's password:
lindapc:~$
```

4. Add 192.168.1.101/24 to the lindapc network interface. Be careful that you don't assign
the same address to both network interfaces.
```
lindapc:~$ sudo ip addr add 192.168.1.101/24 dev eth1
```

5. Use the ping command to test basic network connectivity to a host. From Linda's PC (101) 
ping Bob's PC (100).
```
lindapc:~$ ping 192.168.1.100
PING 192.168.1.100 (192.168.1.100) 56(84) bytes of data.
64 bytes from 192.168.1.100: icmp_seq=1 ttl=64 time=0.052 ms
64 bytes from 192.168.1.100: icmp_seq=2 ttl=64 time=0.037 ms
^C
--- 192.168.1.100 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 0.037/0.044/0.052/0.007 ms
lindapc:~$
```
Hit CTRL-C to stop the output, otherwise it will continue to ping forever.
This command produces a good deal of output and most of it is not relevant to this lab.
We are looking for 0% packet loss. If you pinged the wrong address or there was a configuration
problem, ping would show that is not getting any response back:

```
lindapc:~$ ping 192.168.1.123
PING 192.168.1.123 (192.168.1.123) 56(84) bytes of data.
From 192.168.1.101 icmp_seq=1 Destination Host Unreachable
From 192.168.1.101 icmp_seq=2 Destination Host Unreachable
From 192.168.1.101 icmp_seq=3 Destination Host Unreachable
^C
--- 192.168.1.123 ping statistics ---
5 packets transmitted, 0 received, +3 errors, 100% packet loss, time 4114ms
```


---

## Additional Resources
1. 
