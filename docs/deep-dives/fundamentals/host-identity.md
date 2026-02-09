We return to `pc1` and notice we now see output from the ping command. Every 1 second the ping command sends some data to the 
device at address 192.168.1.2 (pc2) and the recipient sends a reply. If you happened to have the ping running continuously while
troubleshooting the switch configuration, you may have noticed the pings did not start immediately after both ports were enabled.
This has to do with a technology called *spanning tree* and will be covered in future labs. 

## Suggested Resources
- Cisco Press, *CCNA 200-301 Official Cert Guide*, Chapter 1
- O’Reilly, *Computer Networking: A Top-Down Approach*, Section 1.4
- RFC 1122 – Requirements for Internet Hosts
