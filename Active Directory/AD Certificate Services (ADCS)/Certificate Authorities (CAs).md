# Certificate Authorities (CAs) in Active Directory (AD)

### AD CS acknowledges CA certificates in an AD forest through designated containers, each serving unique roles:

#### 1) Certification Authorities container holds trusted root CA certificates.

#### 2) Enrolment Services container details Enterprise CAs and their certificate templates.

#### 3) NTAuthCertificates object includes CA certificates authorized for AD authentication.

#### 4) AIA (Authority Information Access) container facilitates certificate chain validation with intermediate and cross CA certificates.

