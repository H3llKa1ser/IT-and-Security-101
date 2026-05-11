# The Modbus Protocol

## Overview

Modbus is one of the **oldest and most widely used industrial communication protocols**, originally developed by **Modicon (now Schneider Electric) in 1979**. It was designed to allow communication between a **master device** (e.g., SCADA system, HMI) and **slave devices** (e.g., PLCs, RTUs, sensors, actuators).

It remains dominant in ICS/SCADA environments today due to its:
- **Simplicity**
- **Reliability**
- **Open standard (royalty-free)**
- **Massive legacy install base**

---

## Variants of Modbus

| Variant | Medium | Details |
|---|---|---|
| **Modbus RTU** | Serial (RS-232/RS-485) | Binary encoding, compact, most common serial variant |
| **Modbus ASCII** | Serial (RS-232/RS-485) | ASCII encoding, human-readable, older/less efficient |
| **Modbus TCP/IP** | Ethernet (TCP Port 502) | Modbus encapsulated in TCP/IP, most common modern variant |
| **Modbus UDP** | Ethernet (UDP Port 502) | Rare, used where low latency is preferred over reliability |
| **Modbus Plus** | Proprietary Modicon network | Rare, mostly legacy Schneider environments |

---

## How It Works — Master/Slave Architecture

Modbus uses a **request/response** model:

```
Master (SCADA/HMI/PC)          Slave (PLC/RTU/Sensor)
        |                               |
        |------- Request (FC + Data) -->|
        |                               |  (processes request)
        |<------ Response (Data) -------|
```

- **Only the master initiates communication** — slaves never send unsolicited data (in standard Modbus)
- A single master can communicate with **up to 247 slaves** on a serial bus (addresses 1–247)
- Address **0** is the broadcast address (all slaves)
- **Modbus TCP** allows multiple masters and removes the 247 slave limit

---

## Data Model — Four Data Types

Modbus organizes device data into four tables:

| Data Type | Access | Data Size | Address Range | Description |
|---|---|---|---|---|
| **Coils** | Read/Write | 1-bit (Boolean) | 00001–09999 | Digital outputs (e.g., turn a motor ON/OFF) |
| **Discrete Inputs** | Read Only | 1-bit (Boolean) | 10001–19999 | Digital inputs (e.g., switch state) |
| **Input Registers** | Read Only | 16-bit word | 30001–39999 | Analog inputs (e.g., sensor readings) |
| **Holding Registers** | Read/Write | 16-bit word | 40001–49999 | Analog outputs / configuration values |

> 💡 In practice, most implementations use **0-based addressing** internally, so register 40001 = register address 0 in the protocol.

---

## Function Codes (FC)

Function codes tell the slave **what operation to perform**:

### Standard Function Codes
| FC (Hex) | FC (Dec) | Name | Operation |
|---|---|---|---|
| `0x01` | 1 | Read Coils | Read multiple coil (DO) states |
| `0x02` | 2 | Read Discrete Inputs | Read multiple DI states |
| `0x03` | 3 | Read Holding Registers | Read multiple holding registers |
| `0x04` | 4 | Read Input Registers | Read multiple input registers |
| `0x05` | 5 | Write Single Coil | Write a single coil ON/OFF |
| `0x06` | 6 | Write Single Register | Write a single holding register |
| `0x0F` | 15 | Write Multiple Coils | Write multiple coils at once |
| `0x10` | 16 | Write Multiple Registers | Write multiple holding registers |
| `0x11` | 17 | Report Slave ID | Get device info (vendor, model) |
| `0x16` | 22 | Mask Write Register | Bitwise AND/OR on a register |
| `0x17` | 23 | Read/Write Multiple Registers | Combined read and write in one request |
| `0x2B` | 43 | Read Device Identification | Read device identification objects |

### Error/Exception Responses
If a slave can't fulfill a request, it responds with the **original FC + 0x80** (e.g., FC 0x03 error = 0x83), followed by an exception code:

| Exception Code | Meaning |
|---|---|
| `0x01` | Illegal Function Code |
| `0x02` | Illegal Data Address |
| `0x03` | Illegal Data Value |
| `0x04` | Slave Device Failure |

---

## Modbus TCP Packet Structure

A Modbus TCP frame (called an **ADU — Application Data Unit**) looks like this:

```
|<-------- MBAP Header (7 bytes) -------->|<--- PDU --->|
+-----------+-----------+--------+--------+----+--------+
| Trans. ID | Proto. ID | Length | Unit ID| FC | Data   |
| (2 bytes) | (2 bytes) | (2 B)  | (1 B)  |(1B)|(N bytes|
+-----------+-----------+--------+--------+----+--------+
```

| Field | Size | Description |
|---|---|---|
| **Transaction ID** | 2 bytes | Request/response matching (echoed back by slave) |
| **Protocol ID** | 2 bytes | Always `0x0000` for Modbus |
| **Length** | 2 bytes | Number of remaining bytes in the frame |
| **Unit ID** | 1 byte | Slave address (1–247; 0xFF for TCP-only devices) |
| **Function Code** | 1 byte | The requested operation |
| **Data** | Variable | Addresses, quantities, values |

### Example — Read Holding Registers (FC 0x03)
**Request** (Read 2 registers starting at address 0):
```
00 01  00 00  00 06  01  03  00 00  00 02
|TxID| |PrID| |Len | |UI| FC |Addr | |Qty|
```

**Response:**
```
00 01  00 00  00 07  01  03  04  01 F4  00 64
|TxID| |PrID| |Len | |UI| FC |Bc| |Reg1| |Reg2|
```
- Register 1 = `0x01F4` = **500** (e.g., 500 RPM)
- Register 2 = `0x0064` = **100** (e.g., 100°C)

---

## Modbus RTU Packet Structure

For serial Modbus RTU, the frame is simpler:

```
+----------+----+--------+-----+
| Slave ID | FC | Data   | CRC |
| (1 byte) |(1B)|(N bytes)|(2B) |
+----------+----+--------+-----+
```

- **No MBAP header** — just address, function code, data, and a CRC-16 checksum for error detection
- Timing-based framing — a gap of **3.5 character times** marks the end of a frame

---

## Security Weaknesses (Summary)

| Weakness | Impact |
|---|---|
| **No Authentication** | Any device on the network can send commands |
| **No Encryption** | All data transmitted in cleartext — trivially sniffable |
| **No Authorization** | No concept of user roles or permissions |
| **No Message Integrity** | TCP variant has no checksum (relies on TCP); easily MiTM'd |
| **Broadcast Writes** | Unit ID 0 writes affect all slaves simultaneously |
| **No Source Verification** | Slaves can't verify if the master is legitimate |

---

## Quick Interaction with Modbus (Python Example)

```python
from pymodbus.client import ModbusTcpClient

# Connect to a Modbus slave
client = ModbusTcpClient('192.168.1.10', port=502)
client.connect()

# Read 10 holding registers starting at address 0 (slave ID 1)
result = client.read_holding_registers(address=0, count=10, slave=1)
print(result.registers)

# Write a value to holding register 0
client.write_register(address=0, value=1234, slave=1)

# Turn coil 0 ON
client.write_coil(address=0, value=True, slave=1)

client.close()
```

---

## Where Modbus is Used in the Real World

- ⚡ **Power grids** — reading meter data, substation RTUs
- 🏭 **Manufacturing** — PLC communication, conveyor control
- 🛢️ **Oil & Gas** — pipeline monitoring, pump control
- 💧 **Water treatment** — flow meters, valve control
- 🌡️ **HVAC systems** — building automation
- ☀️ **Solar/Wind farms** — inverter and turbine monitoring
- 🚢 **Maritime** — ship systems monitoring

---

## Summary

```
Modbus in a nutshell:
├── Developed: 1979 by Modicon
├── Model: Master/Slave (request/response)
├── Data: Coils (1-bit) + Registers (16-bit)
├── Transport: Serial (RTU/ASCII) or Ethernet (TCP/IP)
├── Port: 502/TCP
├── Security: None (no auth, no encryption, no integrity)
└── Status: Still one of the most deployed ICS protocols globally
```

---

Would you like to go deeper into any aspect — such as **Modbus security attacks**, **packet analysis with Wireshark**, **writing Modbus scripts**, or **setting up a Modbus lab environment**?
