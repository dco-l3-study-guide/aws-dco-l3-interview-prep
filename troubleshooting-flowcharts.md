# AWS DCO — Logical Troubleshooting Flowcharts

> **Note:** These flowcharts illustrate the standard logical troubleshooting methodologies expected during technical scenario questions in the AWS Data Center Operations (DCO) interview loop.

---

## ⚡ Server Won't Power On / No POST

This flow walks through systematic isolation for a server experiencing power failure or POST halt.

```mermaid
graph TD
    A[Symptom: Server Won't Power On / No POST] --> B{Layer 1: Check Power Feed}
    B -->|PDU Out of Power / Cable Loose| C[Reseat Cables / Verify PDU Outlet Status]
    B -->|Power Feed OK| D{Inspect PSU LEDs}
    D -->|Amber / Fault Indicator| E[Swap Faulty Power Supply Unit]
    D -->|Green / Normal Output| F[Check Diagnostic LEDs & BMC Logs]
    F --> G{Error Code Present?}
    G -->|Yes| H[Cross-reference Error Code with Component]
    G -->|No / Ambiguous| I[Reseat Internal Hardware RAM, PCIe Cards]
    I --> J{POST Successful?}
    J -->|Yes| K[Verify System & Close Ticket]
    J -->|No| L[Strip Server to Minimum Configuration]
    L --> M{Powers On in Min Config?}
    M -->|Yes| N[Add Components Back One-by-One to Isolate Fault]
    M -->|No| O[Swap Motherboard / Escalate with Documented Evidence]

