One of the most valued tools in the network professional's toolkit is `ping`. It can be used to check anything from the host sitting
right next to you, to a host located halfway across the planet! There is other information that can be gained from ping, and how it 
works under the hood will be the subject of future labs. 

Before we discuss the configuration of this switch, it helps to define what a switch is on its most basic level. A switch allows
two or more devices to communicate with each other. Could we run a connection directly between pc1 and pc2 and cut out the middle-man? 
Sure, but that doesn't scale well at all. We can use this switch to allow dozens of devices to communicate with each other. This
switch can be connected to other switches to allow hundreds of hosts to exchange data. We can hook one or more of those switches to a
router and connect to other networks, or even the Internet! 

Remember how we said sw1 was **mostly** unconfigured? This was said to prove an interesting point. Switches made by Cisco and Arista
are designed to perform basic switching functions straight out of the box. Just connect the power, plug in two hosts, and you have
yourself a nice little network. Of course, we would want to configure these switches further, and leaving them unconfigured and 
connected to other switches in a corporate network would actually be irresponsible; but we will learn these details in future lessons.

Our first test was to see if pc1 and pc2 could ping each other. If ping isn't working it will show a few lines of information and then
nothing. It will just sit there. If you happened to leave ping running and went to troubleshoot `sw1`, it would have eventually started
showing additional lines of data, roughly one line per second. On linux-based containers like `pc1` and `pc2`, ping doesn't stop until
CTRL-C is pressed.

Since we were told no additional configuration would be needed on the PCs, it was time to connect into `sw1`. Our prompt showed the
hostname and the `>` symbol. This symbol indicates we are in `user EXEC` mode. This is sometimes called unprivileged access. This mode
will provide limited access to functions on the switch. To gain full access, we need to type `enable`. Depending on the configuration,
the switch may ask for an additional password to `privileged EXEC` or enable mode. In this case, there is minimal configuration and we were let straight into the elevated mode, as signified by the `#` in the prompt. 

Most of a network engineer's time in privileged EXEC mode is spent running `show` commands. Just about everything a switch knows can
be discovered through show commands. You will learn to pull out the most important information out of show commands. Other information 
may only be used in deeper troubleshooting, and still further, more obscure information might only make sense to a TAC engineer doing
low-level analysis of your device's problem. 

The first (and only) show command we know so far is `show interface status`. It is a frequently used command on Cisco and Arista
switches because it lists each available port, shows whether that port is operational or not, and gives some general information on
how the port is setup. In this case, the two ports, `Et1` and `Et2` show a status of disabled. When a port is disabled, it is impossible
to know whether a device is connected to it or not. Out of the box, no ports on this switch are disabled, so that means someone (or
maybe something) configured these ports to be in a disabled state. Note: in containerlab only the 2 configured ports show up in this 
output. On the real switch, you would see the total number of ports the switch has. Usually, 8, 16, 24, or 48 ports.

Without over-complicating matters at this point, somebody went into the interface configuration and disabled these ports with the 
`shutdown` command. In most modern Cisco and Arista operating systems, you can negate a command by adding `no` to the front. If we 
want to enable a disabled port, we would use the `no shutdown` command. 

Before configuration on a switch can be changed, we have to enter `global configuration` mode. This can be accomplished with the 
`configure terminal` command, often abbreviated to `conf t`. You will know you are in configuration mode because the prompt will
contain (config). 

Before the first port can be changed, we need to select it using the `interface Et1` command. Notice the prompt changes again to
indicate you're in configuration of interface Et1. From here, the `no shutdown` command can be issued. Note that in Arista EOS, by
default, all changes happen **immediately**. Thus it's important to think through what you're doing **before** you hit enter on 
the command. All network engineers, junior through senior, have regretted hitting enter after it's too late! 

After Et1 has been enabled, repeat the process with Et2. You can enter `interface Et2` from the Et1-config mode and the device
will switch right over to it.

Once these changes have been made, you can type `end` to return to privileged EXEC mode. 

Let's try `show interface status` again. If there is something plugged into both of these ports and all the defaults are fine 
(they are for our example...) the two ports will show a status of `Connected`. 

Before we leave this switch, it's a good idea to save the configuration. Without this extra step, the switch is going to forget
any changes you made when it is power-cycled. To do this, enter `copy run start` (or simply `wr` if you want to look like an
old-school network engineer!) to save the configuration. This command takes what is running on the switch currently (the `running-config`) 
and copies it to what the switch looks for when it boots up (the `startup-config`) but we will discuss these details later on.

We return to `pc1` and notice we now see output from the ping command. Every 1 second the ping command sends some data to the 
device at address 192.168.1.2 (pc2) and the recipient sends a reply. Success!

## Suggested Reading
- Cisco Press, *CCNA 200-301 Official Cert Guide*, Chapter 1
- O’Reilly, *Computer Networking: A Top-Down Approach*, Section 1.4
- RFC 1122 – Requirements for Internet Hosts
