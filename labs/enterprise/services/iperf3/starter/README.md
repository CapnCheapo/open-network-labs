# VLAN Configuration 

## Scenario
Your company has expanded to two floors of the office building. sw1 is deployed to 
the first floor and sw2 is installed on the second. `The cabling team ran a link between
sw1 and sw2 on eth4 of both switches.` 

The user of sales1 is not able to ping sales2. It's the same situation for marketing and
accounting. Devices on the first floor can't seem to ping devices on the second, and vice-
versa. 

Make configuration changes to allow the appropriate communication.

| Team       | Device Name | IP Address    | Switch | Switchport |
| ---------- | ----------- | ------------- | ------ | ---------- |
| Sales      | sales1      | 10.10.102.101 | sw1 | eth1       |
|            | sales2      | 10.10.102.102 | sw2 | eth1      |
| Marketing  | marketing1  | 10.10.103.101 | sw1 | eth2       |
|            | marketing2  | 10.10.103.102 | sw2 | eth2       |
| Accounting | accounting1 | 10.10.104.101 | sw1 | eth3       |
|            | accounting2 | 10.10.104.102 | sw2 | eth3      |


## Tasks
1. Configure the link between sw1 and sw2.
3. Verify PCs of the same type can ping teach other, but cannot ping other PCs.
3. Bonus task: label the eth4 switchports so it's easy for other admins to know what is connected.

## Credentials
Use the following credentials to access each device from your host system.
| Device | Login Command | Password |
| ------ | ------------- | -------- |
| sw1    | ssh admin@clab-vlan-configuration-sw1 | admin |
| sw2    | ssh admin@clab-vlan-configuration-sw2 | admin |
| sales1    | ssh lab@clab-vlan-configuration-sales1 | lab |
| sales2    | ssh lab@clab-vlan-configuration-sales2 | lab |
| marketing1 | ssh lab@clab-vlan-configuration-marketing1 | lab |
| marketing2 | ssh lab@clab-vlan-configuration-marketing2 | lab |
| accounting1    | ssh lab@clab-vlan-configuration-accounting1 | lab |
| accounting2    | ssh lab@clab-vlan-configuration-accounting2 | lab |

## Notes
- L3 functionality is disabled and should not be enabled.
- Do not change any configuration on the hosts.

## Hints (Read Only If Stuck)
1. TBD
