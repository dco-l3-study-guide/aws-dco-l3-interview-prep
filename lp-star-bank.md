# 🎯 AWS Leadership Principles (LP) & STAR Matrix

> **How to Use This Guide:** In the AWS DCO interview loop, behavioral questions carry **70–80%** of the evaluation weight. Every technical story you tell must demonstrate operational maturity, safety compliance, clear ownership, and measurable results.

---

## 🏗️ 1. Customer Obsession 

> **Interviewer Mindset:** *"Does this candidate prioritize rack availability, data integrity, and strict safety over cutting corners to close a ticket fast?"*

### Primary Interview Questions
* *"Tell me about a time you had to balance speed against accuracy or safety during an active outage."*
* *"Describe a situation where a quick fix was requested, but you pushed back for a long-term, safer solution."*
* *"Give an example of how you minimized customer impact during a critical hardware maintenance window."*

### 📐 Story Architecture Blueprint
* **Situation:** High-priority ticket assigned for host flap in production rack.
* **Task:** Isolate fault without causing collateral downtime to adjacent dual-homed servers.
* **Action:** Put on ESD strap ➔ Verified B-feed power redundancy ➔ Identified faulty SFP+ ➔ Replaced optic using clean fiber procedure ➔ Ran loopback test.
* **Result:** Link stabilized with 0 dropped packets; host returned to pool in 18 minutes.

### 💬 Real-World Interview Example
> *"During a high-traffic period, an alarm flagged an enterprise host dropping packets intermittently. The shift manager asked if we could immediately pull and swap the Top-of-Rack network cable to save time. Recognizing that pulling the cable without checking active link aggregation could drop dual-homed traffic for 8 adjacent servers, I pushed back briefly to check the interface status via CLI first. I confirmed the secondary link was active, put on my ESD wrist strap, cleaned the replacement fiber optic ferrules with a click-cleaner, and performed the swap. The link stabilized with zero dropped packets, preventing a broader service impact."*

### 🚩 Red Flags to Avoid
* Skimping on ESD protection or safety checks to meet a fast resolution time.
* Blaming external software teams or end-users for incorrect configurations without verifying hardware state first.

---

## 🔍 2. Dive Deep

> **Interviewer Mindset:** *"Does this candidate stop at swapping a cable, or do they look at metrics, kernel logs, and physical infrastructure to find the true root cause?"*

### Primary Interview Questions
* *"Walk me through a complex technical problem that required deep investigation beyond standard runbooks."*
* *"Tell me about a time an initial diagnosis turned out to be completely wrong. How did you pivot?"*
* *"Give an example of how you used system logs (`dmesg`, IPMI SEL, switch interface counters) to isolate a transient issue."*

### 📐 Story Architecture Blueprint
* **Situation:** Server experiencing sporadic, unexplained reboots every 48–72 hours.
* **Task:** Determine if failure is software-driven, power-related, or a hardware defect.
* **Action:** Checked IPMI SEL logs ➔ Found correctable ECC memory errors on Slot B2 ➔ Performed Slot-vs-Stick RAM test ➔ Confirmed fault followed the DIMM module.
* **Result:** Replaced single bad DIMM stick; server achieved 100% uptime over 90-day observation window.

### 💬 Real-World Interview Example
> *"I was assigned a ticket for a host that kept dropping off the network, but physical link lights remained green. Standard runbooks suggested replacing the network patch cable. Instead of blindly swapping hardware, I logged into the host out-of-band via BMC and ran `dmesg -T` and `ethtool -S eth0`. The interface counters revealed millions of CRC alignment errors, indicating optical degradation rather than a completely broken link. I inspected the fiber ferrule under a microscope, found severe oil contamination, cleaned it, and re-tested signal loss with an Optical Power Meter. Light levels returned to optimal specifications (-3 dBm), resolving the root cause permanently."*

### 🚩 Red Flags to Avoid
* Accepting surface-level fixes (like rebooting a server repeatedly) without determining why it failed.
* Guessing at hardware faults instead of relying on CLI diagnostic output and physical test tools.

---

## 🛠️ 3. Ownership

> **Interviewer Mindset:** *"When something breaks, a safety hazard exists, or documentation is wrong, do they take charge, or do they say 'that's not my shift/queue'?"*

### Primary Interview Questions
* *"Tell me about a time you noticed an issue outside your direct team's responsibility and took charge of fixing it."*
* *"Describe a scenario where a hardware repair regressed or failed post-maintenance. How did you handle it?"*
* *"Give an example of how you improved a messy rack, unlabeled cable run, or inaccurate inventory system."*

### 📐 Story Architecture Blueprint
* **Situation:** Discovered unlabeled fiber patch runs and disorganized power cables during a routine audit.
* **Task:** Eliminate physical trace hazards and risk of accidental cable snags during hot-swaps.
* **Action:** Documented port mappings ➔ Scheduled off-peak maintenance window ➔ Re-routed cables with proper bend radius ➔ Applied standardized port labels.
* **Result:** Improved technician audit time by 25% and eliminated physical snag hazards across 4 racks.

### 💬 Real-World Interview Example
> *"While completing a routine drive replacement in Rack A04, I noticed a PDU power cable hanging loose across an air containment hot-aisle, posing a tripping and snag hazard for anyone servicing nearby chassis. Although it wasn't assigned to my queue, I traced the feed, verified it was supplying redundant B-feed power, and coordinated with the shift lead to re-route and secure the cable using proper Velcro ties. I then updated the rack elevation documentation in our inventory tracking system so future technicians had an accurate physical map."*

---

## ⚡ 4. Bias for Action

> **Interviewer Mindset:** *"Can this technician make high-speed, safe, and calculated decisions when faced with incomplete data during an active alarm?"*

### Primary Interview Questions
* *"Describe a time you had to make a critical operational decision without having all the information you wanted."*
* *"Tell me about an instance where you identified a potential hardware failure before a system monitor alerted."*
* *"How do you prioritize your work queue when multiple critical tickets hit simultaneously?"*

### 💬 Real-World Interview Example
> *"During a night shift, two separate alarms fired at the exact same time: a single storage host drive failure and an ambient thermal warning in Row 3. Recognizing that thermal events pose an immediate threat to an entire row of production servers while a single RAID drive failure is non-disruptive due to parity redundancy, I immediately prioritized the thermal issue. I surveyed the row, identified a blocked airflow damper in the containment aisle, and cleared it. Room temperatures stabilized within 5 minutes, preventing thermal throttling across 40+ servers before I returned to process the drive replacement."*

### 🧠 Two-Way Door vs. One-Way Door Framework
* **Two-Way Door (Reversible Decision):** Swapping a patch cable, testing a spare optical transceiver, or reseating a RAM stick. ➔ *Execute with high urgency and speed.*
* **One-Way Door (Irreversible Decision):** Power-cycling a core switch, wiping RAID arrays, or unseating main power feeds. ➔ *Stop, verify scope, check redundancy, and confirm authorization.*

---

## 🎖️ 5. Insist on the Highest Standards

> **Interviewer Mindset:** *"Does this candidate take pride in clean work, strict adherence to safety guidelines, and error-free execution?"*

### Primary Interview Questions
* *"Tell me about a time you refused to compromise on quality or safety standards, even when under pressure."*
* *"Describe a situation where you caught a mistake made by a colleague or runbook documentation."*

### 💬 Real-World Interview Example
> *"I was performing a motherboard replacement on a high-density compute node. After completing the swap, I noticed that the thermal paste application on the heat sink looked uneven and slightly dried out from a previous installation attempt. Although re-cleaning and re-applying compound would delay the ticket by 15 minutes during a busy shift, I refused to re-install a substandard thermal interface. I cleaned the CPU lid with isopropyl alcohol, applied fresh thermal paste in a proper pattern, and torqued the heatsink to spec. The server passed stress testing with CPU temperatures operating 8°C cooler than baseline averages."*

---

## 📊 Quick-Reference STAR Story Mapping Matrix

| Past Work / Project Experience | Primary LP | Secondary LP | Key Technical Artifacts Included |
| :--- | :--- | :--- | :--- |
| **Intermittent Server Reboot Issue** | Dive Deep | Customer Obsession | IPMI SEL logs, ECC RAM slot-vs-stick isolation |
| **Tripped PDU / Cable Cleanup** | Ownership | Insist on Highest Standards | Rack power balancing, ESD protocols, labeling |
| **Flapping Optical Link Maintenance** | Bias for Action | Dive Deep | VFL laser, optic cleaning, `ethtool` CRC counters |
| **Outdated Handover Runbooks** | Earn Trust | Deliver Results | Inventory audits, shift handover documentation |
| **Thermal Airflow Blockage** | Bias for Action | Customer Obsession | Containment airflow, priority queue management |
