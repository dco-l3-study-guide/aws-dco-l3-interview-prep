# AWS DCO L3 — Leadership Principles & STAR Story Framework

The behavioral component makes up **70–80% of the AWS DCO interview evaluation**. Amazon interviewers evaluate candidates against Amazon's Leadership Principles (LPs) to determine culture fit, operational maturity, and alignment with high performance standards.

---

## 🎯 Priority Leadership Principles for Data Center Operations 

While Amazon has 16 Leadership Principles, DCO panels focus most heavily on the principles listed below.

---

### 1. Customer Obsession
> *Leaders start with the customer and work backwards. They work vigorously to earn and keep customer trust.*

* **DCO Context:** In Data Center Operations, the "customer" is often internal (AWS service teams, compute capacity teams) or external end-users relying on uptime. Protect service availability, respect SLAs, and treat hardware failures with urgency.
* **Key Demonstration Points:**
  * Prioritizing critical ticket queues over administrative tasks.
  * Communicating downtime transparently during high-severity events.
  * Going above and beyond standard runbook requirements to prevent impact.
* **Likely Follow-up Probes:**
  * *"How did you balance customer urgency with safety or protocol compliance?"*
  * *"What trade-offs did you make to meet the deadline?"*

---

### 2. Ownership
> *Leaders are owners. They think long term and don't sacrifice long-term value for short-term results. They act on behalf of the entire company, beyond just their own team. They never say "that's not my job."*

* **DCO Context:** Owning the physical environment. If you notice a loose fiber patch cable, a hazard on the floor, or an unmonitored temperature spike—you fix it or log it, even if it's outside your immediate ticket queue.
* **Key Demonstration Points:**
  * Identifying and resolving an unassigned operational or safety issue.
  * Taking full responsibility when an assigned task encounters unexpected obstacles.
  * Creating documentation or runbook improvements that benefit the entire shift.
* **Likely Follow-up Probes:**
  * *"Why was this your responsibility if it wasn't assigned to you?"*
  * *"How did your actions impact the broader team or facility long term?"*

---

### 3. Earn Trust
> *Leaders listen attentively, speak candidly, and treat others respectfully. They are vocally self-critical, even when doing so is awkward or embarrassing.*

* **DCO Context:** High-stakes infrastructure leaves zero room for cover-ups. If you cause an unintended power drop, mislabel a connection, or damage a rail kit, you must report it immediately so the team can mitigate risk.
* **Key Demonstration Points:**
  * Admitting a mistake immediately to leadership or a senior technician.
  * Rebuilding trust through transparent action and process implementation.
  * Handling a conflict with a teammate professionally and directly.
* **Likely Follow-up Probes:**
  * *"What was the immediate consequence of your mistake?"*
  * *"What specific process did you put in place to ensure it never happened again?"*

---

### 4. Bias for Action
> *Speed matters in business. Many decisions and actions are reversible and do not need extensive study. We value calculated risk taking.*

* **DCO Context:** When a server goes down or a network link drops, quick diagnostic steps prevent larger outages. However, action must be *calculated* and adhere to safety standards—never reckless guessing.
* **Key Demonstration Points:**
  * Making a time-sensitive technical decision with incomplete information.
  * Initiating standard troubleshooting steps swiftly without waiting to be micromanaged.
  * Knowing when to act immediately vs. when to pause and escalate.
* **Likely Follow-up Probes:**
  * *"What risks did you consider before taking action?"*
  * *"What would you have done if your initial action failed or made things worse?"*

---

### 5. Insist on Highest Standards
> *Leaders have relentlessly high standards — many people may think these standards are unreasonably high. Leaders are continually raising the bar and drive their teams to deliver high-quality products, services, and processes.*

* **DCO Context:** High standards mean precise cable management, flawless ESD protection compliance, exact labeling, and comprehensive, timestamped ticket logs.
* **Key Demonstration Points:**
  * Catching a subtle defect, cabling error, or documentation flaw that others missed.
  * Refusing to close a ticket until full operational verification is completed and logged.
  * Setting a higher bar for physical rack cleanliness or ticketing detail.
* **Likely Follow-up Probes:**
  * *"How did others react when you insisted on a higher standard?"*
  * *"How did you measure that the higher standard was maintained over time?"*

---

### 6. Dive Deep
> *Leaders operate at all levels, stay connected to the details, question frequently, and verify. No task is beneath them.*

* **DCO Context:** Not stopping at "part replaced." DCO techs must isolate root causes—determining *why* a DIMM failed, *why* a fiber transceiver dropped light, or *why* a power line tripped.
* **Key Demonstration Points:**
  * Methodically isolating a tricky intermittent hardware or network issue.
  * Analyzing logs (`dmesg`, `journalctl`, BMC logs) to find a non-obvious failure point.
  * Uncovering systemic issues behind recurring tickets.
* **Likely Follow-up Probes:**
  * *"How deep into the technical detail did you personally go?"*
  * *"What data or logs proved your hypothesis was correct?"*

---

## 📐 The STAR Method Framework

```text
SITUATION (15-20%) ──► TASK (10-15%) ──► ACTION (50-60%) ──► RESULT (15-20%)
