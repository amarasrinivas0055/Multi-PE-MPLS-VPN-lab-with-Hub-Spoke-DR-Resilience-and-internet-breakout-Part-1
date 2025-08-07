
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

<img width="1553" height="758" alt="Image" src="https://github.com/user-attachments/assets/d59edde7-3cb3-4081-b31c-5673cdfb5bc4" />

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
| Hub    | HUB   | 10:10  | 100:100     | 200:200, 300:300, 400:400  |
| Spoke1 | SPK1  | 10:10  | 200:200     | 100:100, 300:300, 400:400  |
| Spoke2 | SPK2  | 10:10  | 300:300     | 100:100, 200:200, 400:400  |
| Spoke3 | SPK3  | 10:10  | 400:400     | 100:100, 200:200, 300:300  |

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

HUB & PE1 OUTPUTS :-
==================

HUB To Spoke Reachability :
-------------------------------

<img width="802" height="324" alt="Image" src="https://github.com/user-attachments/assets/1797394a-c2e8-4d49-af2a-ec747cfd537f" />


HUB IP Route :
-----------------

<img width="976" height="887" alt="Image" src="https://github.com/user-attachments/assets/5c492fd3-84b0-42ed-ace5-4336e7ad1b83" />

PE1 To HUB Reachability :
-----------------------------

<img width="747" height="132" alt="Image" src="https://github.com/user-attachments/assets/50bfe426-9016-4a74-874c-56ad3d8d822b" />


PE1 VRF Output :
------------------

<img width="782" height="74" alt="Image" src="https://github.com/user-attachments/assets/d4284f8d-6e56-4053-b418-3cb2a3a663fa" />

PE1 VRF Route Output :
---------------------------

<img width="883" height="118" alt="Image" src="https://github.com/user-attachments/assets/c72d32a3-83fc-4644-ac5d-7ddf02f527e4" />

PE1 MPLS Forwarding Table :
--------------------------------

<img width="951" height="435" alt="Image" src="https://github.com/user-attachments/assets/aab8a8a5-2975-4bff-b9b4-d6694d44a077" />

PE2 & SPOKE 1 OUTPUT :-
==================


Spoke 1 = Spoke 1 to Hub Reachability, Spoke 1 To Other Spoke Reachability, Spoke 1 ip route Outputs :
---------------------------------------------------------------------------------------------------------------------

<img width="1165" height="909" alt="Image" src="https://github.com/user-attachments/assets/80d1f27f-10f7-4968-8235-a85d32ad0383" />


PE2 To Spoke 1 Reachability :
--------------------------------

<img width="793" height="109" alt="Image" src="https://github.com/user-attachments/assets/43074e9e-d627-4c99-a656-8a7a113f3fb6" />


PE2=VRF,VRF Route, MPLS Forwarding Table Output :-
------------------------------------------------------------

<img width="1141" height="1015" alt="Image" src="https://github.com/user-attachments/assets/cc945876-2212-4684-b023-4f02c77c3d4e" />


PE3 & SPOKE 2 OUTPUT :-
==================


Spoke 2 = Spoke 2 to Hub Reachability, Spoke 2 To Other Spoke Reachability, Spoke 2 ip route Outputs :
---------------------------------------------------------------------------------------------------------------------

<img width="985" height="910" alt="Image" src="https://github.com/user-attachments/assets/47b8d1f7-51c1-47e3-8ca3-8ee97b4857e3" />


PE3 To Spoke 2 Reachability :
--------------------------------

<img width="849" height="114" alt="Image" src="https://github.com/user-attachments/assets/4ab97486-173f-4913-a76d-184c7945f703" />


PE 3=VRF,VRF Route, MPLS Forwarding Table Output :-
------------------------------------------------------------

<img width="939" height="998" alt="Image" src="https://github.com/user-attachments/assets/60369927-f025-49e6-bba2-0dc66c9c06e3" />

PE4 & SPOKE 3 OUTPUT :-
==================


Spoke 3 = Spoke 3 to Hub Reachability, Spoke 3 To Other Spoke Reachability, Spoke 3 ip route Outputs :
---------------------------------------------------------------------------------------------------------------------

<img width="1175" height="920" alt="Image" src="https://github.com/user-attachments/assets/9329d584-3c27-46ad-9f11-3864d5e03c48" />


PE 4 To Spoke 3 Reachability :
--------------------------------

<img width="985" height="194" alt="Image" src="https://github.com/user-attachments/assets/be22bda7-42f9-4907-8a74-7d1caa9f03b9" />


PE 4=VRF,VRF Route, MPLS Forwarding Table Output :-
------------------------------------------------------------

<img width="1027" height="950" alt="Image" src="https://github.com/user-attachments/assets/827c04d7-2ba4-435c-93a7-f9f581af2855" />
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
🔗 Connect with me on [LinkedIn](https://www.linkedin.com/in/amara-srinivas-53271a253/recent-activity/all/)

---

## 📎 License

This project is for **educational & demonstration purposes only**.
