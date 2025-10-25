# Multi-Site Enterprise Network Planning and Configuration (GNS3)

## Context

This repository contains the project developed for the **Data Routing (Encaminhamento de Dados)** course unit at the **Coimbra Institute of Engineering (ISEC)** during the 2024/2025 academic year.

## Project Goal

The primary goal was to plan, simulate (using GNS3), and configure a complex, multi-site enterprise network for a fictional organization. This project applies concepts related to advanced IP addressing, various routing protocols, and network security features within a Cisco IOS/IOU environment.

## Network Overview

The simulated network consists of a central Headquarters (Sede - C) interconnected with six distinct branches (Filiais):
* Warehouse (Armazém - A)
* Offices (Escritórios - E)
* Manufacturing (Fabricação - F)
* Store (Loja - L)
* Workshop (Oficina - O)
* Quality Assurance (Qualidade - Q)

Each location features multiple routers and subnets, interconnected via simulated WAN links.

## Key Features & Technologies Implemented

* **IP Addressing:**
    * **IPv4:** Variable Length Subnet Masking (VLSM) applied to the assigned public block (`194.65.152.0/21` based on student ID) for LAN segments.
    * **Private IPv4:** Used strategically for point-to-point links between routers to conserve public address space.
    * **IPv6:** Implemented within the 'Offices' branch (E) using Unique Local Addresses (ULA - `fd00:E::/48`) and **GRE tunneling** for transition/connectivity over the IPv4 infrastructure.
* **Routing Protocols:** A diverse range of protocols was configured across different network segments:
    * **OSPF:** Implemented exclusively in the Headquarters (C) with a **multi-area** design (Areas 0, 1, 2) and **virtual links**.
    * **EIGRP:** Used in the 'Quality' branch (Q - AS 20), 'Offices' branch (E - AS 30 for IPv4 & IPv6), and for the inter-branch connectivity ring (AS 100).
    * **RIPv2:** Configured in the 'Workshop' (O), 'Manufacturing' (F), and 'Store' (L) branches.
    * **Static Routing:** Implemented in the 'Warehouse' (A) branch.
* **Routing Security & Optimization:**
    * **MD5 Authentication:** Configured for all dynamic routing protocols (OSPF, EIGRP, RIPv2) to secure routing updates.
    * **Policy-Based Routing (PBR):** Implemented in the 'Quality' branch (Q) to influence traffic paths based on source address.
    * **Prefix-Lists:** Used in the 'Quality' branch (Q) to filter EIGRP route advertisements.
    * **Route Summarization:** Configured where applicable (e.g., EIGRP in branch Q) to reduce routing table sizes.
* **Basic Router Security:** Standard configurations applied (hostname, password encryption, limited Telnet access with password, MOTD banner).

## Tools Used

* **GNS3 (v2.2.54):** Network simulation platform.
* **Cisco IOU Images:**
    * Router: `i86bi-linux-l3-adventerprisek9-15.4.1T.bin`
    * Switch: Generic GNS3 Ethernet Switch.

## Repository Contents

* `/Relatório ED.pdf`: The detailed project report document **(Note: This document is written in Portuguese)**, covering planning, addressing scheme, configurations, and analysis.
* `/ED2425-2023140947.gns3project`: The portable GNS3 project file containing the full network topology and device configurations. **(Note: IOU image files are NOT included in the project file and must be provided separately in your GNS3 setup)**.

## How to Use

1.  Ensure you have GNS3 installed and configured with the specified Cisco IOU router image (`i86bi-linux-l3-adventerprisek9-15.4.1T.bin`).
2.  Download the `.gns3project` file from this repository.
3.  In GNS3, go to `File > Import portable project` and select the downloaded `.gns3project` file.
4.  Follow the prompts to unpack the project.
5.  Once imported, you should be able to open the project, start the devices, and explore the configurations.

## Author

* João Pedro Vila Pomar 
