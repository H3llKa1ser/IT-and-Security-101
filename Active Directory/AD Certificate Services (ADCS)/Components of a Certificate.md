# Certificate Components

#### 1) The Subject of the certificate denotes its owner.

#### 2) A Public Key is paired with a privately held key to link the certificate to its rightful owner.

#### 3) The Validity Period, defined by NotBefore and NotAfter dates, marks the certificate's effective duration.

#### 4) A unique Serial Number, provided by the Certificate Authority (CA), identifies each certificate.

#### 5) The Issuer refers to the CA that has issued the certificate.

#### 6) SubjectAlternativeName allows for additional names for the subject, enhancing identification flexibility.

#### 7) Basic Constraints identify if the certificate is for a CA or an end entity and define usage restrictions.

#### 8) Extended Key Usages (EKUs) delineate the certificate's specific purposes, like code signing or email encryption, through Object Identifiers (OIDs).

#### 9) The Signature Algorithm specifies the method for signing the certificate.

#### 10) The Signature, created with the issuer's private key, guarantees the certificate's authenticity.

## Special Considerations

### Subject Alternative Names (SANs) expand a certificate's applicability to multiple identities, crucial for servers with multiple domains. Secure issuance processes are vital to avoid impersonation risks by attackers manipulating the SAN specification.
