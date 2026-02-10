# VLAN Configuration 

## Scenario
Your company's systems administrator has configured the following hosts that will be handed out to employees:

| Team       | Device Name | IP Address    | Switchport |
| ---------- | ----------- | ------------- | ---------- |
| Sales      | sales1      | 10.10.101.100 | eth1       |
|            | sales2      | 10.10.101.101 | eth2       |
|            | sales3      | 10.10.101.102 | eth3       |
| Marketing  | marketing1  | 10.10.102.100 | eth4       |
|            | marketing2  | 10.10.102.101 | eth5       |
| Accounting | accounting1 | 10.10.103.100 | eth6       |
|            | accounting2 | 10.10.103.101 | eth7       |
|            | accounting3 | 10.10.103.102 | eth8       |

## Tasks
1. Configure the appropriate VLANs on sw1.
2. Assign the ports to the relevant VLANs.
3. Verify PCs of the same type can ping each other, but cannot ping other PCs.
4. Bonus task: label the switchports so it's easy for other admins to know what is connected.

## Credentials
Use the following credentials to access each device from your host system.
| Device | Login Command | Password |
| ------ | ------------- | -------- |
| sw1    | ssh admin@clab-vlan-configuration-sw1 | admin |
| sales1    | ssh lab@clab-vlan-configuration-sales1 | lab |
| sales2    | ssh lab@clab-vlan-configuration-sales2 | lab |
| sales3    | ssh lab@clab-vlan-configuration-sales3 | lab |
| marketing1 | ssh lab@clab-vlan-configuration-marketing1 | lab |
| marketing2 | ssh lab@clab-vlan-configuration-marketing2 | lab |
| accounting1    | ssh lab@clab-vlan-configuration-accounting1 | lab |
| accounting2    | ssh lab@clab-vlan-configuration-accounting2 | lab |
| accounting3    | ssh lab@clab-vlan-configuration-accounting3 | lab |

## Notes
- Yes, technically this lab works with no configuration changes on the switch, but play along and use VLANs.
- L3 functionality is disabled and should not be enabled.
- Do not change any configuration on the hosts.


## Hints (Read Only If Stuck)
1. TBD
