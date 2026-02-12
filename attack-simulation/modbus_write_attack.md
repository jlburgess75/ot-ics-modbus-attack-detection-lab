attack-simulation/description.md


## Objective
Learn how Modbus TCP works by performing:
1. A normal read operation (Function Code 3)
2. A malicious write operation (Function Code 6)
3. Capture and analyze traffic in Wireshark

---

# Step 1 — Normal Modbus Read

Python code:
```python
from pymodbus.client import ModbusTcpClient
c = ModbusTcpClient("10.0.0.190", port=5020)

resp = c.read_holding_registers(0, 10, unit=1)
print(resp)

