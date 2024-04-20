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

# Converting Kerberos Tickets

### In the Kerberos authentication protocol, ccache and kirbi are two types of Kerberos credential caches that are used to store Kerberos tickets.

 - A credential cache, or "ccache" is a temporary storage area for Kerberos tickets that are
obtained during the authentication process. The ccache contains the user's authentication
credentials and is used to access network resources without having to re-enter the user's
credentials for each request.

 - The Kerberos Integrated Windows Authentication (KIWA) protocol used by Microsoft
Windows systems also makes use of a credential cache called a "kirbi" cache. The kirbi
cache is similar to the ccache used by standard Kerberos implementations, but with some
differences in the way it is structured and managed.

### While both caches serve the same basic purpose of storing Kerberos tickets to enable efficient access to network resources, they differ in format and structure.

