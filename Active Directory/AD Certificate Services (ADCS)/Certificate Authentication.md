# Certificate Authentication

### Active Directory (AD) supports certificate authentication, primarily utilizing Kerberos and Secure Channel (Schannel) protocols.

# Kerberos Authentication Process

 In the Kerberos authentication process, a user's request for a Ticket Granting Ticket (TGT) is signed using the private key of the user's certificate. This request undergoes several validations by the domain controller, including the certificate's validity, path, and revocation status. Validations also include verifying that the certificate comes from a trusted source and confirming the issuer's presence in the NTAUTH certificate store. Successful validations result in the issuance of a TGT. The NTAuthCertificates object in AD, found at:

  - CN=NTAuthCertificates,CN=Public Key Services,CN=Services,CN=Configuration,DC=domain,DC=com

### is central to establishing trust for certificate authentication.

# Secure Channel (Schannel) Authentication

 Schannel facilitates secure TLS/SSL connections, where during a handshake, the client presents a certificate that, if successfully validated, authorizes access. The mapping of a certificate to an AD account may involve Kerberos’s S4U2Self function or the certificate’s Subject Alternative Name (SAN), among other methods.
