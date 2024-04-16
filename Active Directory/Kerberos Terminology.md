# Kerberos Terminology

## 1) Ticket Granting Ticket (TGT)

 - A ticket-granting ticket is an authentication ticket used to request service tickets from the TGS for specific resources from the domain.

## 2) Key Distribution Center (KDC)

 - They Key Distribution Center is a service for issuing TGTs and service tickets that consist of the Authentication Service and the Ticket Granting Service.

## 3) Authentication Service (AS)

 - Issues TGTs to be used by the TGS in the domain to request access to other machines and service tickets

## 4) Ticket Granting Service (TGS)

 - Takes the TGT and returns a ticket to a machine on the domain.

## 5) Service Principal Name (SPN)

 - It is an iedntifier given to a service instance to associate a service instance with a domain service account. Windows requires that services have a domain service account which is why a service needs an SPN set.

## 6) KDC Long Term Key (KDC LT Key)

 - It is based on the KRBTGT service account. It is used to encrypt the TGT and sign the PAC.

## 7) Client Long Term Secret Key (Client LT Key)

 - It is based on the computer or service account. It is used to check the encrypted timestamp and encrypt the session key.

## 8) Service Long Term Secret Key (Service LT Key)

 - It is based on the service account. It is used to encrypt the service portion of the service ticket and sign the PAC.

## 9) Session Key

 - Issued by the KDC when a TGT is issued. The user will provide the session key to the KDC along with the TGT when erquesting a service ticket.

## 10) Privilege Attribute Certificate (PAC)

 - The PAC holds all of the user's relevant information, it is sent along with the TGT to the KDC to be signed by the target LT Key and the KDC LT Key in order to validate the user.
