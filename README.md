# AWS Data Center Operations (DCO) — Complete Interview Study Guide

![Focus: AWS DCO L3](https://img.shields.io/badge/Focus-AWS%20DCO%20L3-orange.svg)
![Type: Public Study Guide](https://img.shields.io/badge/Type-Community%20Prep-blue.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

Welcome to the **AWS Data Center Operations (DCO) Interview Preparation Guide**. This repository is a structured, community-focused study hub designed for candidates preparing for the AWS Data Center Technician interview loop.

> **⚠️ Legal Disclaimer & Compliance:** > This repository contains **strictly publicly available knowledge**, community prep experiences, and general data center engineering concepts. It does **NOT** contain any proprietary Amazon/AWS information, internal system details, confidential runbooks, or actual NDA-protected interview questions. Use this repository strictly as an educational study aid.

---

## 📌 Guide Overview

The AWS DCO interview evaluation is typically divided into two core areas:
* **Behavioral & Leadership Principles (~70–80%):** Evaluates culture fit, safety prioritization, customer focus, operational maturity, and STAR storytelling.
* **Technical Concepts & Logical Troubleshooting (~20–30%):** Evaluates server architecture, hardware isolation, fiber optics, networking layers (L1–L3), and structured problem-solving under pressure.

---

## 🗂️ Documentation Index

Click any module below to dive deep into specific study materials:

### 🧠 1. [Leadership Principles & STAR Story Framework](leadership-principles.md)
* Breakdown of core Leadership Principles prioritized for DCO (Customer Obsession, Ownership, Earn Trust, Dive Deep, Insist on Highest Standards, Bias for Action).
* Strategic STAR method timing guidelines (Situation, Task, Action, Result).
* Interviewer follow-up probe prep and story-mapping matrix.
* Printable STAR story drafting template.

### 🛠️ 2. [Technical Deep-Dive & Hardware Cheat Sheet](docs/technical-cheatsheet.md)
* **Networking:** OSI Model (Layers 1–3), TCP vs. UDP, DHCP (DORA process), DNS.
* **Server Hardware:** POST boot sequence, BMC/IPMI out-of-band management, ECC RAM, slot-vs-stick troubleshooting.
* **Storage & RAID:** HDD vs. SATA/SAS SSD vs. NVMe, RAID 0, 1, 5, 6, and 10 breakdown.
* **Fiber Optics:** Single-Mode (SMF) vs. Multi-Mode (MMF), LC/MPO connectors, transceivers (SFP, QSFP, OSFP), VFL lasers, and optical light meters.
* **Linux CLI:** Essential network (`ip`, `ping`, `traceroute`, `dig`) and hardware (`lsblk`, `lspci`, `dmesg`, `journalctl`) diagnostic commands.

### 🔀 3. [Advanced Troubleshooting Methodology & Flowcharts](docs/troubleshooting-flowcharts.md)
* **Visual Flowcharts (Mermaid.js):** Step-by-step logic for *Server Won't Power On / No POST* and *Network Link Down / Packet Loss*.
* **Physical Isolation:** Minimum configuration testing ("bench testing") and fiber endface inspection/cleaning routines.
* **The 90-Second Response Standard:** Framework for answering technical scenario questions concisely during interview loops.

---

## ⚡ The 6-Step Technical Response Formula

When asked to troubleshoot any technical scenario during the interview, structure your verbal response using this sequence:

1. **Clarify Scope:** Confirm ticket symptoms, affected host(s), and service impact.
2. **Safety First:** Explicitly state ESD strap compliance and physical safety procedures.
3. **Physical Layer Checks (L1):** Inspect PDU power feeds, seating, latching, and physical link lights.
4. **Logical Diagnostics:** Log into out-of-band management (BMC) or review OS system/kernel logs.
5. **Isolate One Variable:** Test or swap **one component at a time** (cables, optics, DIMM slot-vs-stick).
6. **Verify & Document:** Confirm resolution through diagnostic testing, update ticket logs cleanly, and escalate with evidence if out of scope.

---

## 🤝 Contributing & Usage

Feel free to fork this repository, star it if it helps your preparation, or submit a Pull Request if you would like to contribute non-proprietary diagnostic tips or general industry prep resources!

---

## 📄 License

This repository is available under the [MIT License](LICENSE).
