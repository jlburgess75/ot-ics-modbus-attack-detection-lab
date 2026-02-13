# OT/ICS Modbus RTU Write Detection Lab (FC06)

## Executive Summary
This lab demonstrates detection and analysis of **unauthorized Modbus RTU write activity** (Function Code 06) in an industrial control environment.

The project includes:
- Modbus RTU register manipulation simulation
- Terminal-level RTU transaction proof
- Splunk telemetry ingestion (key=value logging)
- Detection engineering logic
- SOC-style incident documentation
- MITRE ATT&CK (ICS) mapping

Designed to showcase OT-aware SOC analyst capability.

---

## Skills Demonstrated
- Industrial protocol analysis (Modbus RTU / RS-485)
- Unauthorized command detection (FC06)
- SIEM ingestion & field extraction (Splunk)
- Detection engineering
- OT business impact analysis
- MITRE ATT&CK (ICS) mapping
- SOC incident documentation workflow

---

## Lab Environment

**Components**
- Raspberry Pi (Modbus RTU client + telemetry forwarder)
- RS-485 Modbus slave device
- Python + minimalmodbus
- Splunk (UDP syslog ingestion)

---

## Attack Scenario – Unauthorized Write (FC06)

Simulated a write to a writable configuration register (`reg=5`).

Workflow:
1. Baseline read (FC03)
2. Unauthorized write (FC06)
3. Verification read (FC03)
4. Splunk ingestion of write event
5. Alert triggered

---

## MITRE ATT&CK (ICS)

| Technique | Description |
|-----------|------------|
| T0855 | Unauthorized Command Message |
| T0831 | Manipulation of Control |
| T0807 | Command-Line Interface |

---

## Business Impact (OT Context)

Unauthorized RTU writes can:
- Manipulate process variables
- Modify configuration parameters
- Cause production disruption
- Create equipment damage or safety risk
- 
  ### Detection Engineering Approach

This lab detects unauthorized Modbus RTU write activity (Function Code 06) by:

1. Logging Modbus transactions as structured key-value telemetry
2. Ingesting events into Splunk SIEM
3. Creating SPL queries to:
   - Detect write function codes (fc=6)
   - Identify unexpected register modifications
   - Alert on abnormal write frequency
4. Triggering a real-time alert for unauthorized write behavior

Example SPL detection:

index=main modbus_rtu_write fc=6
| where reg=5

