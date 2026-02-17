## Getting Started

1. Install containerlab. See the [Containerlab Installation Guide](https://containerlab.dev/install/). The easiest way to 
grab everything at once is to use their quick setup script.

2. Install the necessary images. Commonly-used images are installed as follows:

| Image | Version | How to obtain |
| ----- | ------- | ------------- |
| labhost-lite | Latest | docker pull ghcr.io/capncheapo/labhost-lite:1.0.1 |
| Arista cEOS | Latest | https://www.arista.com/en/support/software-download |
| Cisco IOU | Latest | https://software.cisco.com/download/home/286193282/type/286326381/release/CML-Free |
| Cisco IOU L2 | Latest | https://software.cisco.com/download/home/286193282/type/286326381/release/CML-Free |
| Cisco XRd | Latest | https://software.cisco.com/download/home/286331236/type/280805694/release/25.4.1 |

Arista cEOS can be downloaded for free after creating an Arista account. The Cisco images are subject to 
various license restrictions. **Don't waste your time asking us for images, we will not provide them!**

3. Clone the Open Network Labs repository: 
```
git clone git@github.com:CapnCheapo/open-network-labs.git
```

4. Enter the open-network-labs directory. Labs can be found under the labs directory and documentation under the docs directory.
```
open-network-labs/
├── docs
└── labs
```

5. Each lab follows a consistent structure:
```
lab-name/
├── lab.meta.yml # Metadata (topics, difficulty, prerequisites, etc.)
├── starter/ # Starting point for the learner
│ ├── topology.clab.yml
│ ├── configs/
│ └── README.md
├── solution/ # One possible completed solution
│ ├── topology.clab.yml
│ ├── configs/
│ └── README.md
└── check/ # (Optional) Validation scripts
└── validate.sh
```

6. Starter
The **starter** directory gives you:
- a fully deployed topology
- baseline configurations
- no hidden prerequisites

Your job is to implement the required behavior.

7. Solution
The **solution** directory shows:
- one working implementation
- key configuration choices
- verification commands and example outputs

Solutions are intentionally *not* optimized for minimal config — clarity wins.

8. Validation (optional)
Some labs may include lightweight validation scripts that check outcomes
(e.g., reachability, protocol state, route presence).

Validation checks **results**, not exact configuration syntax.

9. Navigate to the starter directory of the lab you want to start:
```
> cd labs/fundamentals/host-identity/starter
```

10. Use `containerlab deploy` to start the lab. Containerlab will show connection information.
```
> containerlab deploy
17:56:44 INFO Containerlab started version=0.73.0
17:56:44 INFO Parsing & checking topology file=topology.clab.yml
17:56:45 INFO Creating docker network name=clab IPv4 subnet=172.20.20.0/24 IPv6 subnet=3fff:172:20:20::/64 MTU=0
17:56:45 INFO Creating lab directory path=/home/moores/Documents/projects/open-network-labs/labs/fundamentals/host-identity/starter/clab-host-identity
17:56:45 INFO Creating container name=pc3
17:56:45 INFO Creating container name=pc1
17:56:45 INFO Creating container name=pc2
17:56:45 INFO Creating container name=sw1
17:56:46 INFO Created link: sw1:eth1 ▪┄┄▪ pc1:eth1
17:56:46 INFO Created link: sw1:eth3 ▪┄┄▪ pc3:eth1
17:56:46 INFO Running postdeploy actions for Arista cEOS 'sw1' node
17:56:46 INFO Created link: sw1:eth2 ▪┄┄▪ pc2:eth1
17:57:05 INFO Executed command node=pc1 command="sudo ip route del default via 172.20.20.1 dev eth0" stdout=""
17:57:05 INFO Executed command node=pc2 command="sudo ip addr replace 192.168.50.50/24 dev eth1" stdout=""
17:57:05 INFO Executed command node=pc2 command="sudo ip route del default via 172.20.20.1 dev eth0" stdout=""
17:57:05 INFO Executed command node=pc3 command="sudo ip addr replace 192.168.123.100/24 dev eth1" stdout=""
17:57:05 INFO Executed command node=pc3 command="sudo ip route del default via 172.20.20.1 dev eth0" stdout=""
17:57:05 INFO Adding host entries path=/etc/hosts
17:57:05 INFO Adding SSH config for nodes path=/etc/ssh/ssh_config.d/clab-host-identity.conf
╭────────────────────────┬───────────────────────────────────────┬─────────┬───────────────────╮
│          Name          │               Kind/Image              │  State  │   IPv4/6 Address  │
├────────────────────────┼───────────────────────────────────────┼─────────┼───────────────────┤
│ clab-host-identity-pc1 │ linux                                 │ running │ 172.20.20.3       │
│                        │ ghcr.io/capncheapo/labhost-lite:1.0.1 │         │ 3fff:172:20:20::3 │
├────────────────────────┼───────────────────────────────────────┼─────────┼───────────────────┤
│ clab-host-identity-pc2 │ linux                                 │ running │ 172.20.20.5       │
│                        │ ghcr.io/capncheapo/labhost-lite:1.0.1 │         │ 3fff:172:20:20::5 │
├────────────────────────┼───────────────────────────────────────┼─────────┼───────────────────┤
│ clab-host-identity-pc3 │ linux                                 │ running │ 172.20.20.2       │
│                        │ ghcr.io/capncheapo/labhost-lite:1.0.1 │         │ 3fff:172:20:20::2 │
├────────────────────────┼───────────────────────────────────────┼─────────┼───────────────────┤
│ clab-host-identity-sw1 │ arista_ceos                           │ running │ 172.20.20.4       │
│                        │ ceos:4.34.4M                          │         │ 3fff:172:20:20::4 │
╰────────────────────────┴───────────────────────────────────────┴─────────┴───────────────────╯
```

11. Give the lab a minute or two to complete the startup process. 

12. Connect to any lab device using the SSH command:
```
> ssh lab@clab-host-identity-pc1
Warning: Permanently added 'clab-host-identity-pc1' (ED25519) to the list of known hosts.
lab@clab-host-identity-pc1's password: 
pc1:~$
```
| Name | Login | Password |
| ---- | ----- | -------- |
| labhost-lite | lab | lab |
| Arista CEOS | admin | admin |
| Cisco IOU | admin | admin |
| Cisco IOU L2 | admin | admin |
| Cisco XRd | admin | Cisco@123 |

Do not attempt to reconfigure the management interface, or otherwise any interface configured for the 172.20.20.x network. 
This is the management network for your lab and disabling it will make it harder to access your devices.

13. To shut your lab down, run the following command:
```
> containerlab destroy
18:05:03 INFO Parsing & checking topology file=topology.clab.yml
18:05:03 INFO Parsing & checking topology file=topology.clab.yml
18:05:03 INFO Destroying lab name=host-identity
18:05:03 INFO Removed container name=clab-host-identity-pc1
18:05:03 INFO Removed container name=clab-host-identity-pc2
18:05:03 INFO Removed container name=clab-host-identity-pc3
18:05:03 INFO Removed container name=clab-host-identity-sw1
18:05:03 INFO Removing host entries path=/etc/hosts
18:05:03 INFO Removing SSH config path=/etc/ssh/ssh_config.d/clab-host-identity.conf
```

