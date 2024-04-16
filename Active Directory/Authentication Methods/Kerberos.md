# Kerberos Authentication

## Steps:

#### 1) The user sends their username and timestamp encrypted using a key derived from their password to the Key Distribution Center (KDC), a service installed on the Domain Controller in charge of crafting Kerberos tickets on the network.

#### 2) The KDC will create and send back a Ticket Granting Ticket (TGT), which allow the user to request additional tickets to access specific services. The need for a ticket to get more tickets allows users to erquest service tickets without parsing their credentials every time they want to connect to a service. Along with the TGT, a Session Key is given to the user, which they will need to generate the following requests. The TGT is encrypted using the krbtgt account's password hash and therefore the user can't access its contents. It is essential to know that the encrypted TGT includes a copy of the Session Key as part of its contents, and the KDC has no need to store the Session Key as it can recover a copy by decrypting the TGT is needed.

#### 3) When a user wants to connect to a service on the network like a share, website or database, they will use their TGT to ask the KDC for a Ticket Granting Service (TGS). TGS are tickets that allow connection only to the specific service they were created for. To erquest a TGS, the user will send their username and a timestamp encrypted using the Session Key, along with the TGT and a Service Principal Name (SPN), which indicates the service and server name we intend to access.

#### 4) As a result, the KDC will send us a TGS along with a Service Session Key, which we will need to authenticate to the service we want to access. The TGS is encrypted using a key derived from the service owner hash. The service owner is the user or machine account that the service runs under. The TGS contains a copy of the Service Session Key on its encrypted contents so that the service owner can access it by decrypting the TGS.

#### 5) The TGS can then be sent to the desired service to authenticate and establish a connection. The service will use its configured account's password hash to decrypt the TGS and validate the Service Session Key.
