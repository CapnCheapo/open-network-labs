```mermaid
---
title: trunk-configuration
---
graph LR
  sales1["<fa:laptop> sales1"]
  sales2["<fa:laptop> sales2"]
  marketing1["<fa:laptop> marketing1"]
  marketing2["<fa:laptop> marketing2"]
  accounting1["<fa:laptop> accounting1"]
  accounting2["<fa:laptop> accounting2"]
  

  classDef switch fill:#e3f2fd,stroke:#1565c0,stroke-width:2px;
  classDef host fill:#f1f8e9,stroke:#33691e;

  class sw1,sw2 switch
  class sales1,sales2,marketing1,marketing2,accounting1,accounting2 host

  sw1 ---["eth1"] sales1
  sw1 ---["eth2"] marketing1
  sw1 ---["eth3"] accounting1
  sw1 ---["eth4"] sw2

  sw2 ---["eth1"] sales2
  sw2 ---["eth2"] marketing2
  sw2 ---["eth3"] accounting2
```

