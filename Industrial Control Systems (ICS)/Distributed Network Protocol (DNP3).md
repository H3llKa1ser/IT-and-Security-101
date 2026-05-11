# The DNP3 Protocol

## Overview

**DNP3 (Distributed Network Protocol 3)** is an industrial communication protocol developed in **1990 by Westronic (later acquired by GE)**, based on early drafts of the **IEC 60870-5** standard. It was specifically designed for **SCADA communication in electric utilities**, and has since spread to water/wastewater, oil & gas, and other critical infrastructure sectors.

Unlike Modbus (which is extremely simple), DNP3 was built to handle the **harsh realities of real-world SCADA** — unreliable links, large geographic distances, complex data needs, and the requirement for time-stamped events.

It is now maintained by the **DNP Users Group** and is an **IEEE standard (IEEE Std 1815)**.

---

## Why DNP3 Exists — Problems It Solves Over Modbus

| Problem | Modbus Limitation | DNP3 Solution |
|---|---|---|
| **Event-driven data** | Poll-only, no events | Built-in event buffering & reporting |
| **Time synchronization** | No timestamps | Millisecond-accurate timestamps on all data |
| **Unreliable links** | No link-layer integrity | Multi-layer error detection & recovery |
| **Large deployments** | 247 slave limit (serial) | Thousands of outstations supported |
| **Data prioritization** | No priority system | Class 0/1/2/3 data priority system |
| **Unsolicited reporting** | Master must always poll | Outstations can push data when events occur |
| **Complex data types** | Only coils & registers | Analog, binary, counter, time, file, and more |

---

## Where DNP3 is Used

- ⚡ **Electric Utilities** — The dominant protocol for substation automation and SCADA
- 💧 **Water & Wastewater** — Treatment plant and pump station monitoring
- 🛢️ **Oil & Gas** — Pipeline SCADA, remote wellhead monitoring
- 🌊 **Flood & Environmental Monitoring** — Remote sensor networks
- 🚦 **Transportation** — Traffic management systems

---

## Architecture — Master/Outstation Model

DNP3 uses a **Master/Outstation** (not Master/Slave) terminology:

```
Master Station (SCADA/EMS)          Outstation (RTU/IED/PLC)
        |                                       |
        |-------- Request (Poll/Command) ------>|
        |                                       |  (processes)
        |<-------- Response (Data) -------------|
        |                                       |
        |<-------- Unsolicited Report ----------| (outstation-initiated)
```

- **Master**: Central SCADA system, Energy Management System (EMS), or control center
- **Outstation**: RTU, IED (Intelligent Electronic Device), PLC, or smart meter at a remote site
- **Multiple masters** can communicate with the same outstation
- Outstations can send **unsolicited responses** (push data without being polled)

---

## DNP3 Layered Architecture

DNP3 implements a **modified OSI model** called the **EPA (Enhanced Performance Architecture)**:

```
+------------------------------------------+
|         Application Layer                |
|   (Function codes, Object library)       |
+------------------------------------------+
|         Pseudo-Transport Layer           |
|   (Segmentation & reassembly)            |
+------------------------------------------+
|         Data Link Layer                  |
|   (Framing, CRC, addressing)             |
+------------------------------------------+
|         Physical Layer                   |
|   (Serial RS-232/485, TCP/IP, Radio)     |
+------------------------------------------+
```

Each layer has distinct responsibilities — this is what makes DNP3 far more robust than Modbus.

---

## Data Link Layer

The data link layer handles **framing, addressing, and error detection**:

### Frame Structure
```
+-------+--------+-------+--------+--------+--------+-----+
| Start | Length | Ctrl  | Dest   | Source | CRC    | ... |
| 0x0564| (1B)   | (1B)  | (2B)   | (2B)   | (2B)   |     |
+-------+--------+-------+--------+--------+--------+-----+
```

| Field | Size | Description |
|---|---|---|
| **Start Bytes** | 2 bytes | Always `0x05 0x64` — identifies DNP3 frames |
| **Length** | 1 byte | Length of remaining frame |
| **Control** | 1 byte | Direction, frame type, function bits |
| **Destination Address** | 2 bytes | Target outstation address (0–65519) |
| **Source Address** | 2 bytes | Originating device address |
| **CRC** | 2 bytes | CRC-16 checksum for header |
| **Data Blocks** | Variable | Up to 16 bytes per block, each with its own CRC |

> 💡 **Key feature**: Every 16-byte data block has its own **CRC-16 checksum**, providing granular error detection — critical for noisy serial links.

### Data Link Layer Function Codes
| Code | Name | Direction |
|---|---|---|
| `0x00` | ACK | Outstation → Master |
| `0x01` | NACK | Outstation → Master |
| `0x03` | Confirmed User Data | Master → Outstation |
| `0x04` | Unconfirmed User Data | Master → Outstation |
| `0x09` | Request Link Status | Either direction |
| `0x0B` | Status of Link | Response to above |

---

## Transport Layer

The transport layer handles **segmentation and reassembly** of large application messages:

```
+---------+------------------+
| TH Byte | Application Data |
| (1 byte)| (up to 249 bytes)|
+---------+------------------+
```

The single **Transport Header (TH)** byte contains:
- **FIR bit**: First segment of a multi-segment message
- **FIN bit**: Final segment of a multi-segment message
- **Sequence Number**: 6-bit rolling counter for ordering

---

## Application Layer

This is where the **real work happens** — function codes, data objects, and control commands.

### Application Layer Frame Structure
```
+--------+--------+--------+---------+
| AC     | FC     | IIN    | Objects |
| (1B)   | (1B)   | (2B)   | (Var)   |
+--------+--------+--------+---------+
```

| Field | Description |
|---|---|
| **Application Control (AC)** | Sequence number, FIR/FIN bits, confirmation request flag |
| **Function Code (FC)** | The operation being requested/responded |
| **IIN (Internal Indications)** | 16 status bits in responses (errors, device state flags) |
| **Objects** | Data encoded in the DNP3 Object Library format |

---

## Function Codes

### Key Application Layer Function Codes
| FC (Hex) | FC (Dec) | Name | Direction |
|---|---|---|---|
| `0x00` | 0 | Confirm | Master → Outstation |
| `0x01` | 1 | Read | Master → Outstation |
| `0x02` | 2 | Write | Master → Outstation |
| `0x03` | 3 | Select | Master → Outstation |
| `0x04` | 4 | Operate | Master → Outstation |
| `0x05` | 5 | Direct Operate | Master → Outstation |
| `0x06` | 6 | Direct Operate No ACK | Master → Outstation |
| `0x07` | 7 | Freeze | Master → Outstation |
| `0x0D` | 13 | Cold Restart | Master → Outstation |
| `0x0E` | 14 | Warm Restart | Master → Outstation |
| `0x14` | 20 | Enable Unsolicited | Master → Outstation |
| `0x15` | 21 | Disable Unsolicited | Master → Outstation |
| `0x17` | 23 | Record Current Time | Master → Outstation |
| `0x81` | 129 | Response | Outstation → Master |
| `0x82` | 130 | Unsolicited Response | Outstation → Master |

### Select-Before-Operate (SBO)
A critical safety mechanism for control commands:
```
Master                          Outstation
  |--- FC 0x03 (Select) -------->|  "I want to operate output X"
  |<-- FC 0x81 (Response) -------|  "OK, I'm ready"
  |--- FC 0x04 (Operate) ------->|  "Execute!"
  |<-- FC 0x81 (Response) -------|  "Done"
```
This two-step process prevents accidental or single-packet command execution — a key safety feature.

---

## The DNP3 Object Library

DNP3 uses a rich, structured **Object Library** to describe data. Objects are identified by **Group** and **Variation**:

```
Object = Group + Variation + Qualifier + Data
```

### Key Object Groups
| Group | Data Type | Examples |
|---|---|---|
| **Group 1** | Binary Input | Switch state, breaker position |
| **Group 2** | Binary Input Change (Event) | State change with timestamp |
| **Group 3** | Double-bit Binary Input | 4-state input (e.g., breaker: open/closed/intermediate/indeterminate) |
| **Group 10** | Binary Output | Control relay output |
| **Group 12** | Control Relay Output Block (CROB) | Timed pulse, latch ON/OFF commands |
| **Group 20** | Counter | Pulse accumulator (e.g., energy metering) |
| **Group 30** | Analog Input | Sensor readings (voltage, current, temperature) |
| **Group 32** | Analog Input Change (Event) | Analog value change with timestamp |
| **Group 40** | Analog Output Status | Current analog output value |
| **Group 41** | Analog Output Block | Analog output command (e.g., set setpoint) |
| **Group 50** | Time & Date | Time synchronization |
| **Group 60** | Class Objects | Data class polling (Class 0/1/2/3) |
| **Group 70** | File Control | File transfer to/from outstation |
| **Group 80** | Internal Indications | Device status flags |
| **Group 120** | Authentication | DNP3-SA authentication objects |

---

## Data Classes — Priority System

DNP3 organizes data into **four classes** for prioritized polling:

| Class | Purpose | Polling Frequency |
|---|---|---|
| **Class 0** | Static data (current snapshot of all data) | On demand |
| **Class 1** | High-priority events (critical alarms) | Very frequent |
| **Class 2** | Medium-priority events | Frequent |
| **Class 3** | Low-priority events (logs, diagnostics) | Infrequent |

A master can poll "Give me all Class 1 events" to efficiently retrieve only the most critical new data since the last poll — much more efficient than Modbus's brute-force polling.

---

## Unsolicited Responses

One of DNP3's most powerful features — outstations can **push data to the master without being asked**:

```
Outstation                      Master
  |                               |
  | (Event occurs — e.g., breaker trips)
  |                               |
  |--- Unsolicited Response ----->|  FC 0x82, with event data + timestamp
  |<-- Confirm ------------------|  FC 0x00
```

This dramatically reduces bandwidth usage and latency for event notification — critical in power grid protection where a breaker trip must be reported **immediately**.

---

## Timestamps

Every DNP3 event object carries a **48-bit timestamp** with **millisecond precision**:

```
+------------------+
| 48-bit Timestamp |
| ms since epoch   |
| (±1ms accuracy)  |
+------------------+
```

This is essential for:
- **Sequence of Events (SOE)** recording
- **Fault analysis** — determining exact sequence of failures
- **Synchronized phasor measurements** in power grids

---

## DNP3 Secure Authentication (SA)

Because DNP3 was designed with **no security**, the **DNP3 Secure Authentication (DNP3-SA)** extension was added later (now at **Version 5 / IEEE 1815-2012**):

### How It Works
```
Master                          Outstation
  |--- Critical Request -------->|
  |<-- Challenge (random nonce) -|
  |--- HMAC Response ----------->|  (keyed hash of challenge + message)
  |<-- Auth Success / Failure ---|
```

- Uses **HMAC-SHA-256** or **HMAC-SHA-1** for message authentication
- **Challenge-response** prevents replay attacks
- **Update Keys** are used to periodically refresh session keys
- **Critical messages** (control commands) require authentication
- **Non-critical messages** (reads) can be exempt

### SA Weaknesses in Practice
- Many deployments **never enable SA** — too complex to configure
- Some use **weak/default keys**
- **Key management** is difficult across thousands of outstations
- SA **adds latency** — problematic for time-critical grid protection

---

## Internal Indication (IIN) Bits

Every DNP3 response contains a **16-bit IIN word** — a status register for the outstation:

| Bit | Name | Meaning |
|---|---|---|
| IIN 1.0 | `BROADCAST` | Message received via broadcast |
| IIN 1.1 | `CLASS1_EVENTS` | Class 1 events available |
| IIN 1.2 | `CLASS2_EVENTS` | Class 2 events available |
| IIN 1.3 | `CLASS3_EVENTS` | Class 3 events available |
| IIN 1.4 | `NEED_TIME` | Outstation needs time synchronization |
| IIN 1.5 | `LOCAL_CTRL` | Some outputs in local control mode |
| IIN 1.6 | `DEVICE_TROUBLE` | Hardware fault detected |
| IIN 1.7 | `DEVICE_RESTART` | Device has restarted (needs initialization) |
| IIN 2.0 | `NO_FUNC_CODE_SUPPORT` | Function code not supported |
| IIN 2.1 | `OBJ_UNKNOWN` | Requested object unknown |
| IIN 2.2 | `PARAM_ERROR` | Parameter error in request |
| IIN 2.3 | `EVENT_BUFFER_OVERFLOW` | Event buffer has overflowed (events lost) |
| IIN 2.5 | `ALREADY_EXECUTING` | Operation already in progress |
| IIN 2.6 | `CONFIG_CORRUPT` | Configuration corrupt |

> 💡 **Security note**: IIN bits leak significant device state information to any observer on the network.

---

## DNP3 vs Modbus — Comparison

| Feature | Modbus | DNP3 |
|---|---|---|
| **Developed** | 1979 | 1990 |
| **Primary Use** | General industrial | Electric utilities / SCADA |
| **Architecture** | Master/Slave | Master/Outstation |
| **Data Types** | Coils, Registers only | Rich object library (20+ types) |
| **Timestamps** | None | 48-bit millisecond timestamps |
| **Events** | No event system | Full event buffering & classes |
| **Unsolicited** | No | Yes (FC 0x82) |
| **Error Detection** | TCP checksum only | Per-block CRC-16 at every layer |
| **Authentication** | None | Optional DNP3-SA (rarely deployed) |
| **Encryption** | None | None (TLS wrapping possible) |
| **Complexity** | Very simple | Complex, feature-rich |
| **Scalability** | Limited | Thousands of outstations |
| **Port (TCP)** | 502 | 20000 |

---

## Security Weaknesses

| Weakness | Details |
|---|---|
| **No Authentication (default)** | DNP3-SA is optional and rarely deployed — anyone on the network can send commands |
| **No Encryption** | All data including control commands sent in cleartext |
| **Unsolicited Response Spoofing** | Attacker can inject fake unsolicited responses to poison master's view of process state |
| **Replay Attacks** | Without SA, captured command frames can be replayed |
| **Cold/Warm Restart Abuse** | FC 0x0D/0x0E can remotely restart an outstation — potential DoS |
| **Event Buffer Flooding** | Generating excessive events causes `EVENT_BUFFER_OVERFLOW` — real events get dropped |
| **Direct Operate Abuse** | FC 0x05 bypasses Select-Before-Operate safety mechanism |
| **IIN Information Leakage** | Device status, restart events, and configuration issues visible to all |
| **Time Sync Abuse** | FC 0x17/Group 50 can be used to desynchronize outstation clocks, corrupting SOE logs |
| **File Transfer Abuse** | Group 70 file transfer can potentially be used to upload malicious firmware/config |
| **Fuzzing Vulnerabilities** | Many legacy DNP3 parsers crash on malformed frames |

---

## Interacting with DNP3 (Python Example)

Using the **pydnp3** or **opendnp3** library:

```python
# Using dnp3-python (simplified example)
from pydnp3 import opendnp3, openpal, asiopal, asiodnp3

# Create a DNP3 manager
manager = asiodnp3.DNP3Manager(1)

# Create a TCP channel to an outstation
channel = manager.AddTCPClient(
    "tcpclient",
    opendnp3.levels.NORMAL,
    asiopal.ChannelRetry(),
    "192.168.1.10",  # Outstation IP
    "0.0.0.0",
    20000,           # DNP3 port
    PrintingChannelListener()
)

# Create a master station
master = channel.AddMaster(
    "master",
    PrintingSOEHandler(),
    asiodnp3.DefaultMasterApplication(),
    config
)

# Enable the master (starts communication)
master.Enable()

# Perform an integrity poll (read all Class 0 data)
master.ScanAllObjects(
    opendnp3.GroupVariationID(60, 1),  # Class 0
    opendnp3.TaskConfig()
)

# Send a Direct Operate command (turn on a binary output)
crob = opendnp3.ControlRelayOutputBlock(
    opendnp3.ControlCode.LATCH_ON
)
master.DirectOperate(
    crob,
    opendnp3.IndexedValue(crob, 0),  # Output index 0
    PrintingCommandCallback(),
    opendnp3.TaskConfig()
)
```

---

## Wireshark Analysis Tips

```
# DNP3 Wireshark display filters:
dnp3                          # All DNP3 traffic
dnp3.ctl.dir == 1             # Master → Outstation only
dnp3.ctl.dir == 0             # Outstation → Master only
dnp3.app.fc == 5              # Direct Operate commands only
dnp3.app.fc == 130            # Unsolicited responses only
dnp3.app.iin.restart == 1     # Devices that have restarted
dnp3.app.iin.need_time == 1   # Devices needing time sync

# NMAP DNP3 discovery:
nmap -p 20000 --script dnp3-info <target>
```

---

## Summary

```
DNP3 in a nutshell:
├── Developed: 1990 by Westronic (GE)
├── Standard: IEEE 1815
├── Model: Master/Outstation (request/response + unsolicited)
├── Primary Use: Electric utilities, water, oil & gas SCADA
├── Port: 20000/TCP (also serial RS-232/485, radio)
├── Key Features:
│   ├── Rich object library (binary, analog, counter, time, file)
│   ├── 48-bit millisecond timestamps on all events
│   ├── Class 0/1/2/3 data priority system
│   ├── Unsolicited reporting (outstation-initiated)
│   ├── Multi-layer CRC error detection
│   └── Select-Before-Operate safety mechanism
├── Security: None by default (DNP3-SA optional, rarely used)
└── Status: Dominant protocol in electric utility SCADA globally
```


