# MPLS L3VPN Full-Mesh Lab with VRF, Route Reflectors & Mixed PE-CE Routing Protocols

This lab simulates a real-world Service Provider MPLS Layer 3 VPN deployment using **EVE-NG**, integrating **Route Reflectors**, **VRFs**, **MP-BGP**, and a variety of PE-CE routing protocols (Static, RIP, EIGRP, OSPF). It is designed to help understand the interplay of core and customer routing in a scalable and secure SP environment.

---

## 🎯 Objective

Build a scalable and dynamic MPLS L3VPN network that:
- Uses **Route Reflectors** to simplify iBGP mesh
- Implements **VRF separation** for each customer
- Supports **end-to-end reachability**
- Demonstrates **multiple PE-CE routing protocol combinations**
- Allows **inter-customer communication** using extended communities (route targets)

---

## 🧠 Inspired By

This lab was inspired by the excellent tutorial from **Praphul Mishra** (PM Networking), whose content laid the foundation for this design.  
While the original lab used static PE-CE routing, I extended it by introducing **dynamic routing protocols** and **inter-VRF communication** for a more robust and enterprise-scale design.

🙏 Special thanks to **Praphul Mishra** for sharing deep insights into MPLS SP topologies.  
🔗 [Praphul Mishra on LinkedIn](https://www.linkedin.com/in/praphul-mishra-a832b5218/)

---

## 🔧 Technologies Used

- **MPLS** with LDP
- **MP-BGP** (`vpnv4`) for VPN route exchange
- **VRFs** with route distinguishers and route targets
- **Route Reflectors** for iBGP scalability
- **IGP (OSPF)** for P/PE underlay
- **Static, RIP, EIGRP, OSPF** as PE-CE routing protocols
- **Redistribution** between BGP and local protocols

---

## 🧱 Topology Overview

- 6 PE Routers (PE1–PE6)
- 1 P Router
- 2 Route Reflectors (RR1 & RR2)
- 4 Customers (A, B, C, D)
- 2 CE sites per customer (8 CE routers)
- Full iBGP mesh via Route Reflectors
- CE-PE Protocols:
  - Customer A → Static Routing
  - Customer B → RIP
  - Customer C → EIGRP
  - Customer D → OSPF

<img width="1872" height="856" alt="Image" src="https://github.com/user-attachments/assets/c89d2f10-7c93-42b3-adc3-a60bdf624fdb" />

---

## 📘 Lab Concept & Design Summary

- The lab is based on an **MPLS Layer 3 VPN architecture** built in **EVE-NG**, using a combination of **iBGP full-mesh** with **Route Reflectors** for control plane scalability.
- There are **4 unique customers** (Customer A, B, C, D), and each customer has **two CE sites** (Site 1 and Site 2), connected to different PE routers for redundancy and simulation of real-world multi-site customers.

### 🔌 Customer PE-CE Connectivity:
- **Customer A**: Site 1 & 2 connected to **PE1 and PE2** via **Static routing**  
- **Customer B**: Site 1 & 2 connected to **PE3 and PE4** via **RIP**
- **Customer C**: Connected using **EIGRP**
- **Customer D**: Connected using **OSPF**

### 🧠 Design Highlights:
- **Route Reflectors (RR1 & RR2)** are used to simplify the full mesh iBGP VPNv4 peering between PE routers.
  - One RR acts as the **primary** and the other as **backup**, ensuring control plane redundancy.
- **VRFs are configured per customer**, with:
  - Unique Route Distinguishers
  - Multiple `route-target` export and import values
- **All route targets are imported across VRFs**, allowing:
  - **Full-mesh inter-site communication**
  - **Cross-customer communication**, simulating shared services or managed WAN

### 🔧 Protocols and Features Used:
- **MPLS** with LDP for label distribution
- **MP-BGP** for VPNv4 route exchange across PEs
- **OSPF** as the IGP in the SP core
- PE-CE routing: **Static**, **RIP**, **EIGRP**, **OSPF**
- **VRF peer groups** for efficient route-policy management
- **Redistribution** between IGP and BGP as needed
- **End-to-end connectivity verified** between all CE routers across all customer sites

---

## 🧪 How to Use This Lab

1. Import the `.unl` file into your EVE-NG setup.
2. Assign configurations from the `.txt` file to each router.
3. Verify:
   - iBGP VPNv4 neighborship via RRs
   - MPLS label bindings
   - VRF route learning per customer
   - End-to-end pings between CE routers
4. Use commands like:
   - `show ip bgp vpnv4 all`
   - `show ip route vrf <name>`
   - `show mpls forwarding-table`
   - `traceroute vrf <name> <ip>`
     

---

## 📸 Screenshots :-


End To End Reachability :-
=================

<img width="875" height="963" alt="Image" src="https://github.com/user-attachments/assets/ec8b8e19-1d12-4d9e-8c4a-ff1fc028f3c6" />


<img width="1117" height="485" alt="Image" src="https://github.com/user-attachments/assets/c7e65654-0667-4dca-80a3-77deb34e95fd" />


Customer A output screenshots :-
================================

Customer-A-Connected-PE1-CEF :
------------------------------

<img width="671" height="221" alt="Image" src="https://github.com/user-attachments/assets/60939f59-9279-4a3c-ba69-d24cb951b710" />


Customer-A-connected-PE1-forwarding table :
-------------------------------------------

<img width="797" height="410" alt="Image" src="https://github.com/user-attachments/assets/3af54ce5-4f3c-4b07-b82d-b482abaacb8d" />


Customer-A-connected-PE1-MP-BGP-Routes :
----------------------------------------

<img width="854" height="1000" alt="Image" src="https://github.com/user-attachments/assets/87e54c4e-18f6-4297-9b36-5f7d9e3d5ed6" />

Customer-A-site-1-connected-PE1-MP-BGP-Neighborship table :
-----------------------------------------------------------

<img width="902" height="371" alt="Image" src="https://github.com/user-attachments/assets/eef5fefa-d0ee-42d5-9bb6-c1ba3b0ae06b" />


Customer-A-site-1-Static-routes :
---------------------------------

<img width="784" height="340" alt="Image" src="https://github.com/user-attachments/assets/3abb08ba-2bbd-49f7-b92c-5bd264b1aaab" />


Customer-A-Connected-PE2-CEF :
------------------------------

<img width="753" height="217" alt="Image" src="https://github.com/user-attachments/assets/1add4b27-9516-41ed-b45f-f9b93c2c90e2" />


Customer-A-connected-PE2-forwarding table :
-------------------------------------------

<img width="852" height="403" alt="Image" src="https://github.com/user-attachments/assets/d1dee368-824a-4526-b858-30d856908c7c" />


Customer-A-connected-PE2-MP-BGP-Routes :
----------------------------------------

<img width="831" height="984" alt="Image" src="https://github.com/user-attachments/assets/413757f9-fc2a-4a2b-ab78-09858f35169b" />


Customer-A-site-2-connected-PE2-MP-BGP-Neighborship table :
-----------------------------------------------------------

<img width="1052" height="354" alt="Image" src="https://github.com/user-attachments/assets/1e5f0118-2c27-473f-af1e-ebf5da41d8e9" />


Customer-A-site-2-Static-routes :
---------------------------------

<img width="789" height="312" alt="Image" src="https://github.com/user-attachments/assets/651ec27f-ab7a-4246-a888-2d430eb076f5" />


Customer B output screenshots : -
======================

Customer-B-Connected-PE3-CEF :
--------------------------------------

<img width="719" height="234" alt="Image" src="https://github.com/user-attachments/assets/2eb83a00-3c14-430d-b1f6-a7ba4bac717e" />


Customer-B-connected-PE3-forwarding table :
---------------------------------------------------

<img width="888" height="446" alt="Image" src="https://github.com/user-attachments/assets/194785ad-77de-4a60-b795-2920cb8ccebb" />


Customer-B-connected-PE3-MP-BGP-Routes :
---------------------------------------------------

<img width="847" height="941" alt="Image" src="https://github.com/user-attachments/assets/25547665-deab-4042-965d-79874851b45f" />

Customer-B-site-1-connected-PE3-MP-BGP-Neighborship table :
------------------------------------------------------------------------

<img width="966" height="369" alt="Image" src="https://github.com/user-attachments/assets/96565fa0-0731-4859-82f6-ea66d7dade8d" />

Customer-B-site-1-RIP-routes :
----------------------------------

<img width="1060" height="642" alt="Image" src="https://github.com/user-attachments/assets/7d25bcbd-16fe-4a38-afe6-37a930c5474b" />


Customer-B-Connected-PE4-CEF :
--------------------------------------

<img width="846" height="229" alt="Image" src="https://github.com/user-attachments/assets/a1945398-9a9c-4787-9c41-0b2db324e06b" />


Customer-B-connected-PE4-forwarding table :
---------------------------------------------------

<img width="1004" height="435" alt="Image" src="https://github.com/user-attachments/assets/6039aa6d-42dd-4a89-af85-71daa03baa12" />


Customer-B-connected-PE4-MP-BGP-Routes :
---------------------------------------------------

<img width="1004" height="435" alt="Image" src="https://github.com/user-attachments/assets/161bc5cb-82ea-413c-ba83-7d46f9dbc4c0" />


Customer-B-site-2-connected-PE4-MP-BGP-Neighborship table :
------------------------------------------------------------------------

<img width="891" height="355" alt="Image" src="https://github.com/user-attachments/assets/1bf30491-daaf-4eb0-a51e-3666c5c1275f" />


Customer-B-site-2-RIP-routes :
----------------------------------
<img width="1063" height="647" alt="Image" src="https://github.com/user-attachments/assets/ddc122b7-f919-4053-8855-a19f35a30923" />



Customer C output screenshots : -
======================

Customer-C-connected-PE6-forwarding table :-
----------------------------------------------------

<img width="904" height="561" alt="Image" src="https://github.com/user-attachments/assets/e207f466-71fb-49dc-b356-8ed381c67559" />


Customer-C-MP-BGP-routes :
--------------------------------

<img width="1201" height="842" alt="Image" src="https://github.com/user-attachments/assets/9d4a3ec8-4727-4012-87f8-979f48da360a" />


Customer-C-MP-BGP-Neighborship table :
-----------------------------------------------

<img width="1077" height="341" alt="Image" src="https://github.com/user-attachments/assets/0218419a-7593-4c7e-81a6-33bd4d2eef4a" />


Customer-C-site-1-EIGRP-routes :
-------------------------------------

<img width="1010" height="644" alt="Image" src="https://github.com/user-attachments/assets/f46f07d5-e7da-4f45-b346-0466cd84295d" />


Customer-C-site-2-EIGRP-routes :-
------------------------------------

<img width="983" height="640" alt="Image" src="https://github.com/user-attachments/assets/8790f8eb-132c-4979-be50-93d617c6735d" />

Customer D output screenshots : -
======================

Customer-D-connected-PE5-forwarding table :
----------------------------------------------------

<img width="938" height="554" alt="Image" src="https://github.com/user-attachments/assets/96c59a16-607a-4dd7-8d77-e101adcc7b4d" />


Customer-D-MP-BGP-routes :
---------------------------------

<img width="934" height="855" alt="Image" src="https://github.com/user-attachments/assets/0988151d-f3cd-4aaa-8f1c-bc5db654a519" />


Customer-D-MP-BGP-Neighborship table :
-----------------------------------------------

<img width="1040" height="347" alt="Image" src="https://github.com/user-attachments/assets/3c2cab12-4064-4211-96ec-c9fc993ad43f" />


Customer-D-site-1-OSPF-routes :
-------------------------------------

<img width="982" height="644" alt="Image" src="https://github.com/user-attachments/assets/750a2201-9752-4bb2-a2b9-7b2475a55abc" />


Customer-D-site-2-OSPF-routes : 
------------------------------------

<img width="1087" height="660" alt="Image" src="https://github.com/user-attachments/assets/66f7c5f9-f569-4913-bfce-db95320a0512" />


Route Reflector Output Screenshot  : -
========================


Route-reflector-1-MP-BGP-neighborship :
-----------------------------------------------

<img width="1059" height="407" alt="Image" src="https://github.com/user-attachments/assets/6ec4e16c-e9f7-4a5d-bbd4-fe1b4e4b0e27" />


Route-reflector-1-MP-BGP-routes :
--------------------------------------

<img width="1074" height="566" alt="Image" src="https://github.com/user-attachments/assets/f2c1d665-bc35-40b6-a5c0-8a061bbb3881" />


Route-reflector-2-MP-BGP-neighborship : 
----------------------------------------------

<img width="840" height="420" alt="Image" src="https://github.com/user-attachments/assets/921cb526-45cf-4fb0-abef-d7d6dc56934e" />


Route-reflector-2-MP-BGP-routes : 
---------------------------------------

<img width="976" height="590" alt="Image" src="https://github.com/user-attachments/assets/a3506597-5496-42fb-8138-6fe8eb0d20fa" />


Provider-router-forwarding-table :
=======================

<img width="789" height="295" alt="Image" src="https://github.com/user-attachments/assets/56d81a5a-bf26-4c32-a566-697ec795a5be" />


---

## 🚀 What I Learned

This lab deepened my understanding of:

- MPLS VPN architecture in SP environments
- iBGP mesh optimization using Route Reflectors
- VRF route leaking using route-target import/export
- Multi-protocol redistribution techniques
- Building scalable and redundant service provider designs

---

## 🗂 Tags

`MPLS` `MP-BGP` `VRF` `iBGP` `Route Reflector` `OSPF` `RIP` `EIGRP` `Static`  
`Service Provider Lab` `Cisco` `EVE-NG` `CCNP` `CCIE` `Praphul Mishra` `PM Networking`

---

## 📬 Contact

Feel free to reach out to me on [LinkedIn](https://www.linkedin.com/in/amara-srinivas-53271a253/) if you'd like to discuss, collaborate, or provide feedback on this lab.

---
