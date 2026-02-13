# Splunk Detection Logic – Modbus RTU FC06

Events logged as key=value format.

Example:
modbus_rtu_write fc=6 slave=1 reg=5 value=9600 port="/dev/ttyUSB0" status=success

---

## Detection 1 – Any FC06 Write

```spl
index=main modbus_rtu_write fc=6
index=main modbus_rtu_write fc=6 reg=5
index=main modbus_rtu_write fc=6
| bin _time span=1m
| stats count as writes_per_min by slave reg _time
| where writes_per_min > 3
index=main modbus_rtu_write fc=6
| eval hour=strftime(_time,"%H")
| where hour < "06" OR hour > "18"

Commit:


---

# 🔱 PHASE 4 — Incident Report Folder

---

## ✅ STEP 5 — Create incident-report folder

Add file → Create new file

Filename:

