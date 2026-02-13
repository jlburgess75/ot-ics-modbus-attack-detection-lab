# Incident Report: Unauthorized Modbus RTU Write (FC06)

## Analyst
Jerald L. Burgess

## Summary
A Modbus RTU Function Code 06 write was observed targeting register `reg=5` on slave device `slave=1`.

## Timeline
- Baseline read (FC03)
- Unauthorized write (FC06)
- Verification read
- Splunk log ingestion
- Alert triggered

## Evidence
- Python minimalmodbus debug output
- Splunk key=value log event
- Splunk alert trigger

Example Event:
modbus_rtu_write fc=6 slave=1 reg=5 value=9600 port="/dev/ttyUSB0" status=success

## Impact Analysis (OT Context)
In production environments, such writes may:
- Manipulate configuration values
- Alter process control parameters
- Disrupt industrial operations
- Introduce safety risks

## MITRE ATT&CK (ICS)
- T0855 – Unauthorized Command Message
- T0831 – Manipulation of Control

## Recommendations
- Monitor FC06 / FC16 writes
- Alert on sensitive registers
- Restrict serial bus access
- Baseline expected register behavior
