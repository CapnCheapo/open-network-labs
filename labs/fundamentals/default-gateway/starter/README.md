# Default Gateway

## Scenario
The users of `pc1` and `pc2` report that they are unable to connect to the server at `1.1.1.1` and have requested assistance with troubleshooting.

You have been provided the following information:

- `pc1` has the IP address `192.168.1.1`
- `pc2` has the IP address `192.168.1.2`

Your task is to determine why `192.168.1.1` and `192.168.1.2` cannot reach `1.1.1.1` and make any required configuration changes **on the hosts only**.

A more senior network technician informs you that the router for this network is reachable at `192.168.1.100`.

---

## Tasks
1. Verify whether `pc1` and `pc2` can communicate with each other.
2. Verify whether `pc1` and `pc2` can communicate with the server at `1.1.1.1`.
3. Make any necessary configuration changes on `pc1` and `pc2` to restore connectivity.
   - **Do not change any configuration on the switch or router.**

---

## Credentials
Use the following credentials to access each device from your host system.

| Device | Login Command | Password |
| ------ | ------------- | -------- |
| pc1    | `ssh lab@clab-default-gateway-pc1` | `lab` |
| pc2    | `ssh lab@clab-default-gateway-pc2` | `lab` |
| sw1    | `ssh admin@clab-default-gateway-sw1` | `admin` |

---

## Hints (Read Only If Stuck)
1. Basic connectivity testing tools such as `ping` will be useful on `pc1` and `pc2`.
2. Pings issued from `pc1` and `pc2` will run indefinitely until stopped with `CTRL-C`.
3. The host routing table can be viewed using the `ip route` command.
4. Administrative privileges are required to make network configuration changes.
5. Some form of the `sudo ip route` command may be required.
6. `eth0` should be ignored for this lab and must not be modified.
7. `eth1` is the interface used for host communication in this lab.

