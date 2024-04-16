# Kerberos Authentication

## Steps:

#### 1) The user sends their username and timestamp encrypted using a key derived from their password to the Key Distribution Center (KDC), a service installed on the Domain Controller in charge of crafting Kerberos tickets on the network

#### 2) The KDC will create and send back a Ticket Granting Ticket (TGT), which allow the user to request additional tickets to access specific services. The need for a ticket to get more tickets allows users to erquest service tickets without parsing their credentials every time they want to connect to a service. Along with the TGT, a Session Key is given to the user, which they will need to generate the following requests. The TGT is encrypted using the krbtgt account's password hash and therefore the user can't access its contents. It is essential to know that the encrypted TGT includes a copy of the Session Key as part of its contents, and the KDC has no need to store the Session Key as it can recover a copy by decrypting the TGT is needed.

#### 3) 
