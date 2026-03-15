# basic-connectivity

## Scenario
You and your good friend Bob decide you have the best idea for a company ever! Today, in your 
basement, you start Widtastic Widgets, LLC, featuring the widgetiest widgets at the best prices.

Bob has the skill to crank out widgets, while your focus is more on keeping the business running.
You decide it's going to be beneficial to link your two computers together so you can share files.

You found a website that demonstrates how two computers can form a network if they have a CAT5
cable connected between the network ports. It also mentions that both computers need a unique
IP address. It suggests 192.168.1.100/24 and 192.168.1.101/24. Who are you to argue with that?

---

## Tasks
1. Assign 192.168.1.100/24 to lindapc.
2. Assign 192.168.1.101/24 to bobpc.
3. Verify connectivity.

---

## Topology
```mermaid
graph LR
  lindapc---bobpc
```

## Credentials
Use the following credentials to access each device from your host system.

| Device | Login Command | Password |
| ------ | ------------- | -------- |
| lindapc    | `ssh lab@clab-basic-connectivity-lindapc` | `lab` |
| bobpc    | `ssh lab@clab-basic-connectivity-bobpc` | `lab` |

---

## Hints (Read Only If Stuck)
1. Linux lets you assign IP addresses using the command `sudo ip addr add (ip)/(netmask) dev eth1`
2. eth1 is the interface the two PCs are connected to.
3. Do NOT change the eth0 interface, for these labs pretend this interface doesn't exist.
4. The ping command tests for basic network connectivity.
5. Do not provide the netmask when pinging hosts.
6. On linux systems, ping will run until CTRL-C is pressed.
