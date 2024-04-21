# Certificate Enrollment

### The enrollment process for certificates is initiated by an administrator who creates a certificate template, which is then published by an Enterprise Certificate Authority (CA). This makes the template available for client enrollment, a step achieved by adding the template's name to the certificatetemplates field of an Active Directory object.

### For a client to request a certificate, enrollment rights must be granted. These rights are defined by security descriptors on the certificate template and the Enterprise CA itself. Permissions must be granted in both locations for a request to be successful.

# Template Enrollment Rights

### These rights are specified through Access Control Entries (ACEs), detailing permissions like:

#### 1) Certificate-Enrollment and Certificate-AutoEnrollment rights, each associated with specific GUIDs.

#### 2) ExtendedRights, allowing all extended permissions.

#### 3) FullControl/GenericAll, providing complete control over the template.

# Enterprise CA Enrollment Rights

### The CA's rights are outlined in its security descriptor, accessible via the Certificate Authority management console. Some settings even allow low-privileged users remote access, which could be a security concern.

# Additional Issuance Controls

### Certain controls may apply, such as:

#### 1) Manager Approval: Places requests in a pending state until approved by a certificate manager.

#### 2) Enrolment Agents and Authorized Signatures: Specify the number of required signatures on a CSR and the necessary Application Policy OIDs.

# Methods to Request Certificates

### Certificates can be requested through:

#### 1) Windows Client Certificate Enrollment Protocol (MS-WCCE), using DCOM interfaces.

#### 2) ICertPassage Remote Protocol (MS-ICPR), through named pipes or TCP/IP.

#### 3) The certificate enrollment web interface, with the Certificate Authority Web Enrollment role installed.

#### 4) The Certificate Enrollment Service (CES), in conjunction with the Certificate Enrollment Policy (CEP) service.

#### 5) The Network Device Enrollment Service (NDES) for network devices, using the Simple Certificate Enrollment Protocol (SCEP).

### Windows users can also request certificates via the GUI (certmgr.msc or certlm.msc) or command-line tools (certreq.exe or PowerShell's Get-Certificate command).

## Example: 

 - Get-Certificate -Template "User" -CertStoreLocation "cert:\\CurrentUser\\My"
