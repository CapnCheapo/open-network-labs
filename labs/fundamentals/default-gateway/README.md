---
title: default-gateway
---
graph LR
  subgraph gw["192.168.1.100"]
    sw1["<fa:network-wired> sw1"]
  end

  pc1["<fa:laptop> pc1"]
  pc2["<fa:laptop> pc2"]

  classDef switch fill:#e3f2fd,stroke:#1565c0,stroke-width:2px;
  classDef host fill:#f1f8e9,stroke:#33691e;

  class sw1 switch
  class pc1,pc2 host

  sw1 ---|"eth1"| pc1
  sw1 ---|"eth2"| pc2

