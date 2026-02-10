# Address Resolution
## Scenario
This lab is more of a discovery lab rather than a break-fix (although you can "fix" it if you want!)

The question is, if I take a switch out of the box, and plug 3 hosts in, they will be able to ping each other
after the switch completes the boot process.

But why? We didn't assign any IP address to the switch. How is this working at all?

Can the switch ping any of the hosts?

---

## Tasks
1. Verify whether `pc1`, `pc2`, and `pc3` can communicate with each other.
2. Verify whether `sw1` can communicate with the PCs.
3. Make any necessary configuration changes on `pc1` and `pc2` to restore connectivity.
   - **Do not change any configuration changes.**

---

## Credentials
Use the following credentials to access each device from your host system.

| Device | Login Command | Password |
| ------ | ------------- | -------- |
| pc1    | `ssh lab@clab-address-resolution-pc1` | `lab` |
| pc2    | `ssh lab@clab-address-resolution-pc2` | `lab` |
| pc3    | `ssh lab@clab-address-resolution-pc3` | `lab` |
| sw1    | `ssh admin@clab-address-resolution-sw1` | `admin` |

---

## Hints (Read Only If Stuck)
1. Basic connectivity testing tools such as `ping` will be useful.
2. The command `ip neighbor` will be helpful on the PCs.
3. The commands `show ip route` and `show mac address-table` might be useful on sw1.
4. Don't wait very long between ping checks and verification on the switch, or you might miss important information.
