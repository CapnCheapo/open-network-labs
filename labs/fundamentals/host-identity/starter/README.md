# Host Identity

## Scenario
You have been asked to assign `pc1` an IP address in the same subnet as `pc2`. `pc3` should remain inaccessible by both hosts.

You have been provided the following information:

- `pc1` has the IP address ???
- `pc2` has the IP address ???
- `pc3` has the IP address `192.168.123.100`

Your task is to make configuration change(s) on `pc1` so that it can communicate with `pc2` but not `pc3`.
**No configuration should be changed on `pc2`, `pc3`, or `sw1`.**

---

## Tasks
1. Investigate the IP address and netmask of `pc2`.
2. Investigate the IP address and netmask of `pc3`.
3. Assign `pc1` an appropriate IP adddress and netmask.
   - **Do not change any configuration on the other PCs or switch.**
4. Verify `pc1` can ping `pc2`.
5. Verify `pc1` cannot ping `pc3`.

---

## Credentials
Use the following credentials to access each device from your host system.

| Device | Login Command | Password |
| ------ | ------------- | -------- |
| pc1    | `ssh lab@clab-host-identity` | `lab` |
| pc2    | `ssh lab@clab-host-identity-pc2` | `lab` |
| pc3    | `ssh lab@clab-host-identity-pc3` | `lab` |
| sw1    | `ssh admin@clab-host-identity-sw1` | `admin` |

---

## Hints (Read Only If Stuck)
1. `ip address show dev eth1` will show IP configuration on a linux device.
2. Interface eth0 is not directly involved with this lab and should not be changed.
3. A netmask of /24 (255.255.255.0) means the first 3 numbers must match, and the 4th should be unique.
4. Administrative privileges are required to make network configuration changes.
5. The command `sudo ip address add ip/subnet dev eth1` should be used.
