# Kerberos

## Ports: 53 and 88 for TCP and UDP (Uses DNS as well hence the 53 port)

### A network authentication protocol designed form MITs project Athena. Kerberos tries to ensure authentication security in an insecure environment.

### Used in Windows 2000+ and some Unix

### Allows for Single Sign-On

### Uses symmetric encryption to verify identifications

### Avoids replay attacks

## Kerberos components

### Authentication Server (AS): Allows authentication of the user and issues a TGT

### Ticket Granting Service (TGS): After receiving the TGT from the user, the TGS issues a ticket for a particular user to access a particular service

### Key Distribution Center (KDC) = A system which runs the TGS and the AS

### Ticket: Means of distributing session key

### Principles (users, applications, services)

### Kerberos software

### Main goal: User needs to authenticate himself without sending passwords across the network, needs to prove he knows the password without actually sending it across the wire.

## Kerberos Concerns

### Computers must have clocks synchronized within 5 minutes of each other

### Tickets are stored on the workstation. If the workstation is compromised, your identity can be forged.

### If your KDC is hacked, security is lost

### A single KDC is a single point of failure and performance bottleneck

### Still vulnerable to password guessing attacks
