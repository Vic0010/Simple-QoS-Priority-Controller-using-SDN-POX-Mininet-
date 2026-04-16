# Simple QoS Priority Controller using SDN (POX + Mininet)

## Project Title

**Simple QoS Priority Controller using SDN Rules**

---

## Problem Statement

This project demonstrates a **Software Defined Networking (SDN) based QoS controller** using **POX** and **Mininet**. The controller prioritizes selected traffic types by assigning different **OpenFlow priority values**.

* **h1 → h3** traffic is treated as **high priority**
* **h2 → h3** traffic is treated as **low priority**
* Explicit **match–action flow rules** are installed by the controller
* Reverse path rules are added for bidirectional communication

This shows how SDN can be used to classify and prioritize traffic flows dynamically.

---

## Tools & Technologies

* **Ubuntu (WSL)**
* **Mininet**
* **POX Controller**
* **Open vSwitch**
* **Python**
* **OpenFlow 1.0**

---

## Topology Used

* **h1** → High priority client
* **h2** → Low priority client
* **h3** → Server / destination host
* **s1** → OpenFlow switch
* **POX** → Remote controller

Topology command:

```bash
sudo mn --topo single,3 --mac --switch ovsk --controller remote
```

---

##  Project Files

```text
pox/
└── pox/
    └── misc/
        └── qos_controller.py
```

---

## Execution Steps

### 1) Run Controller

```bash
cd ~/pox
python3 pox.py misc.qos_controller
```

### 2) Start Mininet

```bash
sudo mn --topo single,3 --mac --switch ovsk --controller remote
```

### 3) Test Connectivity

```bash
h1 ping -c 5 h3
h2 ping -c 5 h3
```

### 4) Verify Flow Rules

```bash
sh ovs-ofctl dump-flows s1
```

---

## Expected Output

The flow table should show:

* `priority=100` for **h1 → h3**
* `priority=10` for **h2 → h3**
* reverse path rules for h3 back to h1 and h2

Sample proof:

```text
priority=100,in_port=s1-eth1
priority=10,in_port=s1-eth2
```

---



## 👨‍💻 Author

**Vikas R**
