# Kerberos Tickets

### Tickets are used to grant access to network resources. A ticket is a data structure that contains information about the user's identity, the network service or resource being accessed, and the permissions or privileges associated with that resource. Kerberos tickets have a limited lifetime and expire after a set period of time, typically 8 to 12 hours.

### There are two types of tickets in Kerberos:

## Ticket Granting Ticket (TGT)

 - The TGT is obtained by the user during the initial
authentication process. It is used to request additional service tickets without requiring the
user to re-enter their credentials. The TGT contains the user's identity, a timestamp, and an
encryption of the user's secret key.

## Service Ticket (ST)

 - The service ticket is used to access a specific network service or
resource. The user presents the service ticket to the service or resource, which then uses
the ticket to authenticate the user and grant access to the requested resource. The service
ticket contains the user's identity, a timestamp, and an encryption of the service's secret
key.
