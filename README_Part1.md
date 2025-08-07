
# 🚀 Multi-PE MPLS VPN Lab – Part 1: Hub-Spoke with RT Manipulation

## 📘 Overview

This lab simulates a real-world **MPLS Layer 3 VPN Hub-and-Spoke design** using **EVE-NG**. It is Part 1 of a multi-stage project, focused on building the **foundation of an MPLS VPN service** with **spoke-to-spoke isolation** using **MP-BGP VPNv4** and **Route Target (RT) control**.

> ⚙️ Technologies: MPLS, MP-BGP, OSPF, VRF, Route Distinguisher, Route Target, LDP

---

## 🎯 Objective

- Establish **Hub-and-Spoke communication** across 5 PE routers.
- Ensure **Spokes can only communicate with the Hub**, not with each other.
- Use **MP-BGP VPNv4** to exchange customer routes between PEs.
- Configure **RT import/export rules** to manipulate routing behavior.

---

## 🧱 Topology

- **1 Hub (CE)** router (R6)
- **3 Spoke (CE)** routers (R7, R8, R9)
- **5 PEs** (R1–R5)
- **MPLS Core** with full LDP and IGP
- **VRFs** configured per customer site

![Topology](topology.png)

---

## 🧠 Technologies Used

| Component       | Protocol / Feature      |
|----------------|--------------------------|
| Transport      | MPLS (LDP)               |
| PE-PE Routing  | MP-BGP (VPNv4)           |
| PE-CE Routing  | OSPF                     |
| Segmentation   | VRF with RD/RT           |
| Route Control  | RT Import/Export         |
| Platform       | EVE-NG                   |

---

## ⚙️ Route Target Manipulation Logic

| Site   | VRF   | RD     | Export RT | Import RT       |
|--------|-------|--------|-----------|------------------|
| Hub    | HUB   | 10:10  | 10:10     | 11:11, 12:12... |
| Spoke1 | SPK1  | 11:11  | 11:11     | 10:10            |
| Spoke2 | SPK2  | 12:12  | 12:12     | 10:10            |
| Spoke3 | SPK3  | 13:13  | 13:13     | 10:10            |

🔒 **Spoke-to-Spoke communication is blocked** since Spokes do not import each other’s RTs.

---

## 🔍 Key Verifications

- ✅ Hub learned all Spoke routes via MP-BGP
- ✅ MPLS forwarding-table shows correct labels
- ✅ Spokes learned Hub routes only
- ✅ Spokes unable to reach each other (intentional isolation)
- ✅ End-to-End pings successful (Hub ↔ Spokes)

---

## 📸 Screenshots (Outputs)

- `Hub IP Route` – All spoke loopbacks reachable via BGP
- `Spoke1 to Hub Ping` – Success
- `Spoke1 to Spoke2 Ping` – Fails (as designed)
- `MPLS Forwarding Table` – Correct label bindings
- `VRF Route Tables` – Proper RT filtering

---

## 📂 Folder Structure

```bash
mpls-l3vpn-hub-spoke-part1/
├── README.md
├── topology.png
├── Multi-PE-MPLS-VPN-Hub-Spoke.unl
├── configs/
│   ├── PE1.txt
│   ├── PE2.txt
│   ├── HUB.txt
│   ├── SPK1.txt
│   └── ...
├── outputs/
│   ├── hub-ip-route.png
│   ├── spk1-reachability.png
│   ├── pe1-vrf-output.png
│   └── ...
```

---

## 🚧 What’s Next?

### ✅ Part 2: DR Site and Resilience with Sham-Link
- Add a DR site and create **OSPF Sham-Link** between DR ↔ Hub
- Introduce **failover routing** when Hub loses PE connectivity

### 🌐 Part 3: Internet Breakout & NAT
- Provide Internet access to Spokes via Hub
- **NAT failover** using two ISPs (Hub and DR)

---

## 🙌 Credits

Created by **Amara Srinivas** – Network Engineer & Lab Enthusiast  
🔗 Connect with me on [LinkedIn](https://www.linkedin.com)

---

## 📎 License

This project is for **educational & demonstration purposes only**.
