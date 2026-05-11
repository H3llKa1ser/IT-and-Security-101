# OLE for Process Control (OPC)

## Overview

**OPC (OLE for Process Control)** is a set of **standardized software interfaces and protocols** that enable **interoperability between industrial automation software and hardware** from different vendors. It was developed in **1996** by a task force of industrial vendors (including Fisher-Rosemount, Rockwell, Opto 22, Intellution, and Intuitive Technology) in collaboration with **Microsoft**.

The name comes from **OLE (Object Linking and Embedding)** — a Microsoft technology that OPC originally relied upon. Over time, OPC evolved far beyond OLE, and the **OPC Foundation** now governs the standard.

> 💡 Think of OPC as a **universal translator** between industrial devices (PLCs, RTUs, DCS) and software applications (SCADA, HMI, historians, MES systems) — regardless of manufacturer.

---

## The Problem OPC Solves

Before OPC, every SCADA/HMI vendor had to write **custom drivers** for every PLC/device they wanted to support:

```
WITHOUT OPC (Pre-1996):
┌─────────┐    Custom Driver    ┌─────────┐
│  SCADA  │◄──────────────────►│  PLC A  │
│ Vendor A│    Custom Driver    │ Vendor X│
│         │◄──────────────────►│  PLC B  │
│         │    Custom Driver    │ Vendor Y│
│         │◄──────────────────►│  RTU C  │
└─────────┘                    │ Vendor Z│
                               └─────────┘
= N×M custom drivers needed (combinatorial explosion)
```

```
WITH OPC:
┌─────────┐                   ┌──────────┐    ┌─────────┐
│  SCADA  │   OPC Standard    │  OPC     │    │  PLC A  │
│ Vendor A│◄─────────────────►│  Server  │◄──►│ Vendor X│
│  HMI   │   OPC Standard    │ (Vendor  │◄──►│  PLC B  │
│ Vendor B│◄─────────────────►│  Driver) │◄──►│  RTU C  │
│Historian│   OPC Standard    │          │    │         │
│ Vendor C│◄─────────────────►│          │    │         │
└─────────┘                   └──────────┘    └─────────┘
= One OPC server per device family, any client connects
```

---

## OPC Family of Standards

OPC has evolved into a **family of specifications**, split into two generations:

### Generation 1 — OPC Classic (1996–2006)
Built on **Microsoft DCOM (Distributed Component Object Model)**

| Standard | Full Name | Purpose |
|---|---|---|
| **OPC DA** | OPC Data Access | Real-time process data read/write |
| **OPC HDA** | OPC Historical Data Access | Access to historical/archived data |
| **OPC AE** | OPC Alarms & Events | Alarm and event subscription/notification |
| **OPC DX** | OPC Data eXchange | Server-to-server data exchange |
| **OPC XML-DA** | OPC XML Data Access | XML/SOAP-based DA over HTTP |
| **OPC Batch** | OPC Batch | Batch process data (ISA-88) |
| **OPC Security** | OPC Security | Basic security for Classic OPC |

### Generation 2 — OPC UA (2006–Present)
**OPC Unified Architecture** — completely rewritten, platform-independent

| Standard | Details |
|---|---|
| **OPC UA** | Unified, cross-platform, secure successor to all Classic specs |
| **OPC UA PubSub** | Publish/Subscribe extension (MQTT/AMQP transport) |
| **OPC UA FX** | Field eXchange — OPC UA for field-level devices |
| **OPC UA over TSN** | Time-Sensitive Networking for deterministic communication |

---

## OPC Classic (DA) — Deep Dive

### Architecture

```
┌─────────────────────────────────────────┐
│           OPC Client Application        │
│      (SCADA, HMI, Historian, MES)       │
└────────────────┬────────────────────────┘
                 │  DCOM/COM Interface
┌────────────────▼────────────────────────┐
│             OPC DA Server               │
│  ┌──────────────────────────────────┐   │
│  │         OPC Address Space        │   │
│  │  ┌────────┐  ┌────────────────┐  │   │
│  │  │ Group1 │  │     Items      │  │   │
│  │  │        │  │ Tag1: 75.3°C   │  │   │
│  │  │        │  │ Tag2: 1200 RPM │  │   │
│  │  └────────┘  │ Tag3: ON/OFF   │  │   │
│  └──────────────┴────────────────┴──┘   │
│             Device Driver               │
└────────────────┬────────────────────────┘
                 │  Protocol (Modbus/S7/etc.)
┌────────────────▼────────────────────────┐
│         Physical Device (PLC/RTU)       │
└─────────────────────────────────────────┘
```

### Key Concepts

#### OPC Items
The basic unit of data — represents a **single process variable** (tag):

| Property | Description |
|---|---|
| **ItemID** | Unique identifier (e.g., `Channel1.Device1.Temperature`) |
| **Value** | The actual data value (VARIANT type) |
| **Quality** | Data quality indicator (Good/Bad/Uncertain) |
| **Timestamp** | When the value was last updated |

#### OPC Groups
Clients organize items into **groups** for efficient polling:

```
OPC Group (UpdateRate: 500ms)
├── Item: "PLC1.Tank1.Temperature"    → 85.3°C   [GOOD]
├── Item: "PLC1.Tank1.Pressure"       → 2.4 bar  [GOOD]
├── Item: "PLC1.Tank1.Level"          → 67.2%    [GOOD]
└── Item: "PLC1.Pump1.Speed"          → 1450 RPM [UNCERTAIN]
```

#### Data Quality Codes
| Quality | Code | Meaning |
|---|---|---|
| **Good** | 0xC0 | Data is valid and current |
| **Uncertain** | 0x40 | Data validity questionable |
| **Bad** | 0x00 | Data is invalid |
| **Bad - Comm Failure** | 0x18 | Communication to device lost |
| **Bad - Device Failure** | 0x0C | Device reported failure |

### OPC DA Interfaces (COM)

OPC Classic exposes **COM interfaces** that clients call:

| Interface | Purpose |
|---|---|
| `IOPCServer` | Server management, group creation |
| `IOPCItemMgt` | Add/remove/validate items in a group |
| `IOPCSyncIO` | Synchronous read/write operations |
| `IOPCAsyncIO2` | Asynchronous read/write with callbacks |
| `IOPCGroupStateMgt` | Manage group properties (update rate, etc.) |
| `IOPCBrowseServerAddressSpace` | Browse available tags on the server |
| `IOPCItemProperties` | Read item metadata/properties |

### How OPC DA Communication Works

```
1. CLIENT CONNECTS:
   Client → CoCreateInstance(OPC Server CLSID) → Server

2. BROWSE ADDRESS SPACE:
   Client → IOPCBrowseServerAddressSpace::Browse() → Tag list

3. ADD GROUP:
   Client → IOPCServer::AddGroup("MyGroup", UpdateRate=1000ms)

4. ADD ITEMS TO GROUP:
   Client → IOPCItemMgt::AddItems(["Tag1", "Tag2", "Tag3"])

5. READ DATA:
   Option A - Synchronous:
   Client → IOPCSyncIO::Read() → {Value, Quality, Timestamp}

   Option B - Subscription (Async):
   Server → IOPCDataCallback::OnDataChange() → Client (on change)

6. WRITE DATA:
   Client → IOPCSyncIO::Write(TagID, NewValue) → Server → Device
```

---

## OPC Classic — DCOM Architecture & Problems

OPC Classic is built entirely on **Microsoft DCOM**, which creates significant challenges:

### How DCOM Works
```
Client Machine                    Server Machine
┌─────────────┐                  ┌─────────────┐
│ OPC Client  │                  │  OPC Server │
│             │    DCOM/RPC      │             │
│  COM Proxy  │◄────────────────►│  COM Stub   │
│             │   TCP (dynamic   │             │
│             │   ports 1024+)   │             │
└─────────────┘                  └─────────────┘
```

### DCOM Problems
| Problem | Details |
|---|---|
| **Windows Only** | DCOM is a Microsoft technology — OPC Classic runs only on Windows |
| **Dynamic Ports** | DCOM uses dynamically assigned ports (1024–65535), making firewall rules a nightmare |
| **DCOM Configuration** | Complex DCOM security settings (DCOMCNFG) frequently misconfigured |
| **Firewall Unfriendly** | Nearly impossible to pass through strict firewalls — led to "punch holes everywhere" culture |
| **No Native Encryption** | DCOM traffic is unencrypted by default |
| **Authentication Issues** | Relies on Windows NTLM/Kerberos — credential relay attacks possible |
| **No Cross-Platform** | Linux, embedded devices, and cloud systems can't natively host OPC Classic |

---

## OPC UA — Unified Architecture (Deep Dive)

OPC UA (released 2006, IEC 62541) was a **complete redesign** that addresses all OPC Classic limitations.

### Design Principles
- ✅ **Platform Independent** — runs on Windows, Linux, macOS, embedded, cloud
- ✅ **Built-in Security** — authentication, encryption, and integrity by design
- ✅ **Unified** — replaces DA, HDA, AE in a single specification
- ✅ **Extensible Information Model** — object-oriented, semantic data modeling
- ✅ **Scalable** — from embedded microcontrollers to enterprise cloud systems
- ✅ **Firewall Friendly** — uses fixed ports (4840/TCP default)

### OPC UA Architecture

```
┌───────────────────────────────────────────────────────┐
│                    OPC UA Client                      │
│           (SCADA, MES, Cloud, Analytics)              │
└─────────────────────┬─────────────────────────────────┘
                      │  OPC UA Services
┌─────────────────────▼─────────────────────────────────┐
│                  OPC UA Server                        │
│  ┌─────────────────────────────────────────────────┐  │
│  │              Information Model                  │  │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────┐  │  │
│  │  │  Objects │  │Variables │  │    Methods   │  │  │
│  │  │  (Nodes) │  │ (Values) │  │ (Callable)   │  │  │
│  │  └──────────┘  └──────────┘  └──────────────┘  │  │
│  └─────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────┐  │
│  │           Communication Stack                   │  │
│  │  UA Binary │  UA XML │  UA JSON │  PubSub       │  │
│  └─────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────┐  │
│  │              Security Layer                     │  │
│  │  Certificates │ Encryption │ Signing │ Auth     │  │
│  └─────────────────────────────────────────────────┘  │
└─────────────────────┬─────────────────────────────────┘
                      │  Device Drivers
┌─────────────────────▼─────────────────────────────────┐
│              Physical Devices (PLCs, RTUs)             │
└───────────────────────────────────────────────────────┘
```

### OPC UA Information Model

Unlike OPC Classic's flat tag list, OPC UA uses a **hierarchical, object-oriented node model**:

#### Node Types
| Node Class | Description | Example |
|---|---|---|
| **Object** | Container/instance | `Tank1`, `Pump1`, `Reactor` |
| **Variable** | Data point with value | `Temperature`, `Speed`, `Status` |
| **Method** | Callable function | `StartPump()`, `ResetAlarm()` |
| **ObjectType** | Class definition | `TankType`, `PumpType` |
| **VariableType** | Variable template | `AnalogItemType` |
| **DataType** | Data type definition | `Float`, `Boolean`, `Structure` |
| **ReferenceType** | Defines relationships | `HasComponent`, `HasProperty` |
| **View** | Filtered address space subset | Operator view, maintenance view |

#### Node Attributes
Every node has:
```
NodeId          → Unique identifier (ns=2;s=Tank1.Temperature)
BrowseName      → Human-readable name
DisplayName     → Localized display name
Description     → Documentation string
NodeClass       → Object/Variable/Method/etc.
Value           → (Variables only) the actual data
DataType        → Float, Int32, Boolean, String, etc.
AccessLevel     → Read, Write, ReadWrite, HistoryRead
Historizing     → Whether history is being collected
```

#### Example Address Space
```
Root
└── Objects
    └── Plant1
        ├── Tank1 [Object]
        │   ├── Temperature [Variable: Float = 85.3]
        │   ├── Pressure    [Variable: Float = 2.4]
        │   ├── Level       [Variable: Float = 67.2]
        │   └── FillTank()  [Method]
        └── Pump1 [Object]
            ├── Speed       [Variable: Int32 = 1450]
            ├── Status      [Variable: Boolean = True]
            └── Start()     [Method]
            └── Stop()      [Method]
```

### OPC UA Services

OPC UA defines **service sets** (like API endpoints):

| Service Set | Services | Purpose |
|---|---|---|
| **Discovery** | FindServers, GetEndpoints | Find OPC UA servers |
| **Secure Channel** | OpenSecureChannel, CloseSecureChannel | Establish encrypted channel |
| **Session** | CreateSession, ActivateSession, CloseSession | User authentication & sessions |
| **Node Management** | AddNodes, DeleteNodes | Modify address space |
| **Browse** | Browse, BrowseNext, TranslateBrowsePathsToNodeIds | Navigate address space |
| **Read** | Read | Read node attributes/values |
| **Write** | Write | Write node values |
| **Subscription** | CreateSubscription, ModifySubscription, DeleteSubscriptions | Event/data subscriptions |
| **Monitored Items** | CreateMonitoredItems, ModifyMonitoredItems | Subscribe to specific nodes |
| **Method** | Call | Execute methods on server |
| **History** | HistoryRead, HistoryUpdate | Access historical data |
| **Query** | QueryFirst, QueryNext | Query address space |

### OPC UA Communication Flow

```
1. DISCOVERY:
   Client → FindServers(DiscoveryURL) → List of OPC UA servers

2. GET ENDPOINTS:
   Client → GetEndpoints(ServerURL) → Security policies & endpoints

3. OPEN SECURE CHANNEL:
   Client ←→ Server: TLS-like handshake
   Exchange certificates, agree on security policy

4. CREATE SESSION:
   Client → CreateSession(ClientCert, SessionName) → SessionId

5. ACTIVATE SESSION:
   Client → ActivateSession(UserIdentityToken) → Authenticated

6. BROWSE ADDRESS SPACE:
   Client → Browse(RootNode) → Child nodes, recursively

7. READ DATA:
   Client → Read([NodeId1, NodeId2, ...]) → [{Value, Quality, Timestamp}]

8. SUBSCRIBE TO CHANGES:
   Client → CreateSubscription(PublishingInterval=500ms)
   Client → CreateMonitoredItems([NodeId1, NodeId2])
   Server → Publish() → Client (when values change)

9. WRITE DATA:
   Client → Write(NodeId, NewValue) → StatusCode

10. CALL METHOD:
    Client → Call(ObjectNodeId, MethodNodeId, [InputArgs]) → [OutputArgs]

11. CLOSE SESSION & CHANNEL:
    Client → CloseSession() → CloseSecureChannel()
```

---

## OPC UA Security Model

This is where OPC UA shines over OPC Classic:

### Security Layers

```
┌────────────────────────────────────┐
│         Application Layer          │
│   User Authentication & AuthZ      │ ← Who are you? What can you do?
├────────────────────────────────────┤
│         Session Layer              │
│   Application Authentication       │ ← Is this a trusted application?
├────────────────────────────────────┤
│         Secure Channel             │
│   Encryption + Message Signing     │ ← Is data private & unmodified?
├────────────────────────────────────┤
│         Transport Layer            │
│   TCP / HTTPS / WebSockets         │
└────────────────────────────────────┘
```

### Security Policies
| Policy URI | Signing | Encryption | Key Size |
|---|---|---|---|
| `None` | None | None | — |
| `Basic128Rsa15` | RSA-SHA1 | AES-128 CBC | 1024-bit ⚠️ (deprecated) |
| `Basic256` | RSA-SHA1 | AES-256 CBC | 2048-bit ⚠️ (deprecated) |
| `Basic256Sha256` | RSA-SHA256 | AES-256 CBC | 2048-bit ✅ |
| `Aes128_Sha256_RsaOaep` | RSA-SHA256 | AES-128 CTR | 2048-bit ✅ |
| `Aes256_Sha256_RsaPss` | RSA-SHA256-PSS | AES-256 CTR | 2048-bit ✅ (recommended) |

### User Authentication Methods
| Method | Details |
|---|---|
| **Anonymous** | No authentication — anyone can connect ⚠️ |
| **Username/Password** | Basic credentials (encrypted over secure channel) |
| **X.509 Certificate** | PKI-based mutual authentication ✅ |
| **Kerberos** | Windows domain authentication |
| **JWT Token** | Modern token-based auth (newer implementations) |

### Application Authentication (Certificates)
```
Client Certificate          Server Certificate
┌────────────────┐          ┌────────────────┐
│ Common Name    │          │ Common Name    │
│ Thumbprint     │◄────────►│ Thumbprint     │
│ Valid From/To  │  Mutual  │ Valid From/To  │
│ Key Usage      │  Trust   │ Key Usage      │
│ Signed by CA   │          │ Signed by CA   │
└────────────────┘          └────────────────┘
```
Both client and server **exchange and validate certificates** — preventing man-in-the-middle attacks.

---

## OPC UA Transports

| Transport | Details | Use Case |
|---|---|---|
| **UA Binary (opc.tcp://)** | Compact binary encoding over TCP port 4840 | Primary — most efficient |
| **UA HTTPS (https://)** | UA XML or JSON over HTTPS port 443 | Firewall-friendly, web integration |
| **UA WebSockets (opc.wss://)** | Binary over WebSockets | Browser clients, cloud |
| **PubSub / MQTT** | Publish-Subscribe over MQTT broker | IoT, cloud, one-to-many |
| **PubSub / AMQP** | Publish-Subscribe over AMQP | Enterprise messaging |
| **PubSub / UDP Multicast** | Multicast for local networks | Low-latency LAN |

---

## OPC UA PubSub

A newer extension to OPC UA adding **Publish/Subscribe** alongside the traditional client/server model:

```
Traditional Client/Server:        PubSub Model:
                                  
Client ←→ Server                  Publisher → Broker → Subscriber1
(one-to-one, connected)           (one-to-many, decoupled)
                                       ↓         → Subscriber2
                                    (MQTT/AMQP)  → Subscriber3
```

Benefits:
- **Scalable** — one publisher, many subscribers
- **Decoupled** — publisher doesn't know subscribers
- **Cloud-ready** — integrates with MQTT brokers (AWS IoT, Azure IoT Hub)
- **Bandwidth efficient** — only publish changes

---

## OPC Classic vs OPC UA Comparison

| Feature | OPC Classic (DA) | OPC UA |
|---|---|---|
| **Released** | 1996 | 2006 |
| **Platform** | Windows only | Cross-platform |
| **Transport** | DCOM (dynamic ports) | TCP 4840, HTTPS 443 |
| **Firewall** | Very unfriendly | Friendly |
| **Security** | Minimal (Windows auth only) | Built-in TLS, PKI, auth |
| **Encryption** | None | AES-256 |
| **Data Model** | Flat tag list | Rich OO node model |
| **Semantics** | No (just tag names) | Full semantic model |
| **HDA Support** | Separate OPC HDA spec | Built-in |
| **Alarms** | Separate OPC AE spec | Built-in |
| **Scalability** | Limited | Embedded to cloud |
| **Complexity** | Simple | Complex but powerful |
| **Status** | Legacy (still widely deployed) | Active, growing |

---

## Security Weaknesses & Misconfigurations

### OPC Classic Weaknesses
| Weakness | Details |
|---|---|
| **DCOM Attack Surface** | DCOM exposes a massive Windows RPC attack surface |
| **NTLM Relay** | DCOM authentication uses NTLM, vulnerable to relay attacks |
| **No Encryption** | All OPC Classic traffic is cleartext |
| **Dynamic Ports** | Forces wide-open firewall rules (1024–65535) |
| **Over-Permissive DCOM** | "Everyone - Full Control" DCOM settings common to fix connectivity |
| **Windows Vulnerabilities** | Unpatched Windows OPC servers vulnerable to OS-level exploits |
| **OPC Enum Tools** | Tools like OPC Scout/OPC Browser trivially enumerate all tags |

### OPC UA Misconfigurations
| Misconfiguration | Details |
|---|---|
| **Security Policy: None** | No encryption or authentication — anyone can read/write |
| **Anonymous Authentication** | No user credentials required to connect |
| **Self-Signed Certs Trusted Blindly** | Servers accept any certificate without validation |
| **Expired/Weak Certificates** | SHA-1 or 1024-bit RSA certificates still in use |
| **No Certificate Revocation** | Revoked certificates still accepted |
| **Excessive Permissions** | Anonymous users given write access |
| **Exposed on Internet** | Port 4840 accessible from internet (Shodan: `port:4840`) |
| **No Audit Logging** | Write operations not logged — no forensic trail |
| **Default Demo Servers** | Test/demo OPC UA servers left running in production |

---

## Tools for OPC

### Discovery & Enumeration
| Tool | Purpose |
|---|---|
| **Prosys OPC UA Browser** | GUI browser for OPC UA servers |
| **UaExpert (Unified Automation)** | Feature-rich OPC UA client for exploration |
| **OPC Scout** | OPC Classic enumeration |
| **opcua-client-gui** | Open-source OPC UA GUI client |
| **Shodan** | `port:4840` finds internet-exposed OPC UA servers |

### Programming & Testing
| Tool | Purpose |
|---|---|
| **python-opcua / asyncua** | Python OPC UA client/server library |
| **node-opcua** | Node.js OPC UA implementation |
| **open62541** | C/C++ OPC UA stack (open-source) |
| **FreeOpcUa** | Free Python OPC UA server for testing |
| **Prosys OPC UA Simulation Server** | Free simulation server for testing |

### Security Testing
| Tool | Purpose |
|---|---|
| **opcua-exploit-framework** | OPC UA security testing |
| **Wireshark** | OPC UA dissector built-in |
| **scapy** | Custom OPC UA packet crafting |
| **metasploit** | OPC-related modules |

---

## Quick Python Example (OPC UA)

```python
from opcua import Client

# Connect to OPC UA server
client = Client("opc.tcp://192.168.1.10:4840")

# Set security (for a properly secured server)
client.set_security_string(
    "Basic256Sha256,SignAndEncrypt,client_cert.pem,client_key.pem"
)

try:
    client.connect()
    
    # Get root node and browse
    root = client.get_root_node()
    print("Root children:", root.get_children())
    
    # Read a node by NodeId
    node = client.get_node("ns=2;s=Tank1.Temperature")
    value = node.get_value()
    print(f"Temperature: {value}°C")
    
    # Write a value
    node = client.get_node("ns=2;s=Pump1.Speed")
    node.set_value(1500)
    
    # Browse address space
    objects = client.get_objects_node()
    for child in objects.get_children():
        print(child.get_browse_name())

    # Subscribe to data changes
    from opcua import ua
    
    class DataChangeHandler:
        def datachange_notification(self, node, val, data):
            print(f"Node {node} changed to {val}")
    
    handler = DataChangeHandler()
    sub = client.create_subscription(500, handler)
    sub.subscribe_data_change(node)

finally:
    client.disconnect()
```

---

## Where OPC is Used in the Real World

- 🏭 **Manufacturing** — Connecting PLCs to MES and ERP systems
- ⚡ **Power Utilities** — Substation data to SCADA/EMS
- 🛢️ **Oil & Gas** — Upstream/downstream process data aggregation
- 💧 **Water Treatment** — Plant-wide data integration
- 🏗️ **Building Automation** — BMS to enterprise systems
- ☁️ **Industry 4.0 / IIoT** — OPC UA as the bridge from OT to cloud
- 🤖 **Robotics** — OPC UA built into modern robot controllers (KUKA, FANUC, ABB)
- 🚗 **Automotive** — Factory automation and quality systems

---

## Summary

```
OPC in a nutshell:
├── Purpose: Universal interoperability standard for industrial automation
├── Created: 1996 (OPC Classic), redesigned 2006 (OPC UA)
├── Governed by: OPC Foundation
│
├── OPC Classic:
│   ├── Based on: Microsoft DCOM/COM
│   ├── Platform: Windows only
│   ├── Security: Poor (no encryption, DCOM auth only)
│   ├── Variants: DA, HDA, AE, DX
│   └── Status: Legacy, still widely deployed
│
└── OPC UA:
    ├── Based on: Custom stack (platform independent)
    ├── Platform: Windows, Linux, macOS, embedded, cloud
    ├── Security: Built-in TLS, PKI certificates, user auth
    ├── Transport: TCP 4840, HTTPS, WebSockets, MQTT/AMQP
    ├── Model: Object-oriented semantic node model
    ├── Standard: IEC 62541
    └── Status: Active standard, rapidly growing adoption
```

