# AWS DCO L3 — Technical Deep-Dive & Hardware Cheat Sheet

> **Scope Note:** This technical guide covers fundamental Data Center Operations concepts across server hardware, physical Layer 1 infrastructure, fiber optics, basic networking, and Linux CLI diagnostic utilities.

---

## 🌐 Networking & OSI Fundamentals

### The OSI Model (Focus on Layers 1–3)

| Layer | Name | Data Unit | Key Components & Concepts |
| :--- | :--- | :--- | :--- |
| **Layer 1** | Physical | Bits | Fiber optics, CAT6 cables, transceivers (SFP/QSFP), power distribution (PDUs), rack units. |
| **Layer 2** | Data Link | Frames | MAC addresses, switches, Top-of-Rack (ToR) switches, VLAN tagging, ARP, Ethernet frames. |
| **Layer 3** | Network | Packets | IP addresses (IPv4/IPv6), routers, ICMP (`ping`), routing tables, subnets, gateways. |

---

### Core Network Protocol Breakdown

#### 1. TCP vs. UDP
* **TCP (Transmission Control Protocol):** Connection-oriented protocol using a 3-way handshake (`SYN` $\rightarrow$ `SYN-ACK` $\rightarrow$ `ACK`). Guarantees reliable, ordered, and error-checked delivery. Used for SSH, HTTP/HTTPS, and file transfers.
* **UDP (User Datagram Protocol):** Connectionless, lightweight protocol. Sends packets without handshakes or delivery confirmation. Prioritizes low latency over reliability. Used for DNS queries, video streaming, and NTP.

#### 2. DHCP (Dynamic Host Configuration Protocol)
Automates IP address assignment. Uses the **DORA** process:
1. **D**iscover: Client broadcasts a request to find a DHCP server.
2. **O**ffer: DHCP server offers an available IP address.
3. **R**equest: Client requests to lease the offered IP address.
4. **A**cknowledge: Server confirms the lease and sends subnet mask, default gateway, and DNS addresses.

#### 3. DNS (Domain Name System)
Translates human-readable domain names into numerical IP addresses. Key diagnostic tools include `dig` and `nslookup`.

---

## 🖥️ Server Hardware Architecture & Memory

### Power-On Self-Test (POST) & Boot Process
1. **Power Sequence:** Power Supply Unit (PSU) stabilizes power rails and sends a `Power_Good` signal to the motherboard.
2. **Execution:** The CPU executes the BIOS/UEFI firmware code from flash memory.
3. **Hardware Checks:** POST checks primary components:
   * System memory (RAM DIMM detection and capacity verification).
   * CPU presence and thermal check.
   * PCIe bus and expansion cards.
   * Storage controllers (RAID cards/HBAs).
4. **Halt / LED Error Code:** If POST fails, the server halts execution and outputs error codes via diagnostic LEDs, POST codes, or BMC event logs.

---

### IPMI & Baseboard Management Controller (BMC)
* **BMC:** An independent service processor embedded on server motherboards. Operates out-of-band (OOB), meaning it remains active even if the main server CPU, OS, or primary power state is off.
* **Capabilities:** Remote power control (power cycle, hard shutdown), reading thermal/voltage sensors, monitoring system event logs (SEL), and providing virtual KVM redirection over a dedicated network interface.

---

### Hardware Components Breakdown

```text
               ┌────────────────────────────────────────────────────────┐
               │                SERVER ARCHITECTURE MAP                 │
               ├────────────────────────────────────────────────────────┤
               │  [ CPU ] ◄──────► [ System Memory / RAM (DIMMs) ]      │
               │    │                                                   │
               │    ├───────────► [ PCIe Bus (NICs, HBAs, Accelerators) ]│
               │    │                                                   │
               │    └───────────► [ Storage Controller / NVMe Direct ]  │
               │                            │                           │
               │             ┌──────────────┴──────────────┐            │
               │             ▼                             ▼            │
               │    [ HDD / SATA SSD ]             [ NVMe SSDs ]        │
               │    (SAS/SATA Bus)                 (PCIe High-Speed)    │
               └────────────────────────────────────────────────────────┘

#### Memory (RAM / DIMMs)
* **ECC Memory (Error-Correcting Code):** Standard in enterprise servers. Detects and corrects single-bit memory errors on the fly to prevent kernel panics and data corruption.
* **Troubleshooting Slot vs. Stick:** If a DIMM slot is unrecognized:
  1. Reseat the DIMM.
  2. Swap the suspected bad DIMM with a known-good slot to isolate whether the failure follows the **slot** (motherboard/CPU socket issue) or the **stick** (faulty RAM).

#### Storage Technologies

| Storage Type | Medium | Bus / Protocol | Latency | Key Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **HDD** | Spinning Platters | SATA / SAS | High (~10ms) | Mass cold storage / archiving |
| **SSD** | Solid-State Flash | SATA / SAS | Medium (~100µs) | Standard boot drives & OS workloads |
| **NVMe** | Solid-State Flash | PCIe Direct | Low (~10–30µs) | High-performance databases & caching |

---

### RAID Array Reference
* **RAID 0 (Striping):** Combines drives for performance. No fault tolerance. Single drive failure results in complete data loss.
* **RAID 1 (Mirroring):** Duplicates data across paired drives. Provides 100% redundancy with a 50% storage capacity penalty.
* **RAID 5 (Striping + Parity):** Requires minimum 3 drives. Spreads parity data across all drives. Withstands a single drive failure.
* **RAID 6 (Double Parity):** Requires minimum 4 drives. Uses dual parity blocks to withstand up to two simultaneous drive failures.
* **RAID 10 (Striped Mirrors):** Combines RAID 1 redundancy with RAID 0 performance. Requires minimum 4 drives.

---

## 🔌 Fiber Optics & Infrastructure Mechanics

### Fiber Optic Cable Types

| Feature | Single-Mode Fiber (SMF) | Multi-Mode Fiber (MMF) |
| :--- | :--- | :--- |
| **Jacket Color** | Yellow | Aqua / Erika Violet |
| **Core Diameter** | ~9 microns (Narrow) | 50 or 62.5 microns (Wide) |
| **Light Source** | Laser | Light-Emitting Diode (LED) / VCSEL |
| **Distance Range** | Long distances (Kilometers) | Short distances (Data center intra-rack runs) |

---

### Common Fiber Connectors & Transceivers

#### Connectors
* **LC (Lucent Connector):** Standard duplex push-and-pull connector used in server network interfaces and patch panels.
* **MPO/MTP (Multi-fiber Push On):** High-density array connector housing 8, 12, or 24 individual fiber strands within a single physical plug.

#### Transceivers
Plug-in optical modules that interface host equipment to fiber cabling:
* **SFP / SFP+:** Small Form-Factor Pluggable (1Gbps / 10Gbps).
* **QSFP+ / QSFP28:** Quad Small Form-Factor Pluggable (40Gbps / 100Gbps).
* **OSFP / QSFP-DD:** Ultra-high-density optics (400Gbps+ speeds).

---

### Physical Layer Diagnostic Tools
* **VFL (Visual Fault Locator):** A high-powered visible red laser tool connected to fiber strands to detect physical micro-bends, cracks, or complete line breaks visually.
* **Optical Power Meter (OPM):** Measures light signal strength (dBm) to verify optical loss is within operational tolerance thresholds.
* **Fiber Scope / Inspection Probe:** Used to inspect fiber endfaces for microscopic dust or oil contamination prior to mating connectors.

---

## 🐧 Essential Linux Networking & Diagnostic Commands

### Interface & Network Configuration
```bash
# Display all network interfaces, assigned IP addresses, and link states
ip addr show

# Display routing tables and configured default gateways
ip route show

# Verify Layer 3 network reachability to a target host
ping -c 4 <ip_address_or_hostname>

# Trace packet path hop-by-hop to isolate network latency or drop points
traceroute <target_ip>

# Query DNS server to resolve hostname to IP address
dig <domain_name>
nslookup <domain_name>
