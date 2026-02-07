# Basic L2 Connectivity

## Introduction
Welcome to the very first lab in the series!

This lab is intentionally simple. If you already have the skills required to install containerlab, deploy this topology, and connect to the devices, 
you may not learn any *new* technical concepts here. In that case, treat this lab as an entry point into the Open Network Labs workflow and 
conventions.

If you are truly new to networking, you may need help getting started. Ask a friend or colleague to help you deploy the lab and connect to the 
devices. Do not expect to understand everything immediately. Even engineers with many years of experience often discover gaps in their understanding 
when revisiting fundamentals.

During the fundamentals labs, we will establish a set of practical “rules” that help you reason about networks. As you progress, you will learn when
these rules can be bent—and eventually, when they can be broken to solve edge cases. This progression mirrors how most engineers actually learn 
networking over time.

Work through the lab, ask questions when you get stuck, and feel free to explore beyond the stated tasks. Break things. Fix them. With a single 
command, you can always redeploy the lab back to its original state.

## Scenario
You are a junior network technician with a simple task: two hosts must be able to communicate with each other.

A colleague hands you a switch that she believes is **mostly** unconfigured. She connects `pc1` to port 1 and `pc2` to port 2. She tells you that:
- `pc1` has the IP address `192.168.1.1`
- `pc2` has the IP address `192.168.1.2`

Each host treats its IP address like a home mailing address. If a message is addressed correctly and placed on the network, it should arrive at its 
destination.

Your task is to determine whether communication is possible—and if not, why.

## Tasks
1. Verify whether or not the two hosts can communicate with each other.
2. If they cannot communicate, connect to `sw1` and perform basic verification.
3. Make any necessary configuration changes on the switch to allow communication.
   **Do not change any configuration on the hosts**

## Credentials
Use the following credentials to access each device from your host system.
| Device | Login Command | Password |
| ------ | ------------- | -------- |
| pc1    | ssh lab@clab-basic-l2-connectivity-pc1 | lab |
| pc2    | ssh lab@clab-basic-l2-connectivity-pc2 | lab |
| sw1    | ssh admin@clab-basic-l2-connectivity-sw1 | admin |


## Hints (Read Only If Stuck)
1. Basic connectivity testing tools such as `ping` will be useful on `pc1` and `pc2`.
2. Pings on `pc1` and `pc2` will run indefinitely until `CTRL-C` is pressed.
3. On `sw1`, entering privileged mode (`enable`) allows access to diagnostic commands.
4. Interface status can be viewed using commands that show port state.
5. Configuration mode is required to make changes to the switch.
6. Interfaces may be administratively disabled.
7. Changes may take a short time to take effect—be patient.
