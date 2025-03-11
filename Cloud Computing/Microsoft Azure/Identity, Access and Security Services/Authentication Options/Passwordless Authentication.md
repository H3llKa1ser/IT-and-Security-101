# Passwordless Authentication

Features like multifactor authentication (MFA) are a great way to secure your organization, but users often get frustrated with the additional security layer on top of having to remember their passwords. Passwordless authentication methods are more convenient because the password is removed and replaced with something you have, plus something you are or something you know.

Each organization has different needs when it comes to authentication. Microsoft Azure and Azure Government offer the following four passwordless authentication options that integrate with Microsoft Entra ID:

1) Windows Hello for Business

2) Microsoft Authenticator

3) Passkeys FIDO2 (Fast IDentity Online 2)

4) Certificate-based authentication

## Windows Hello for Business

Windows Hello for Business is ideal for information workers that have their own designated Windows PC. The biometric and PIN credentials are directly tied to the user's PC, which prevents access from anyone other than the owner. With public key infrastructure (PKI) integration and built-in support for single sign-on (SSO), Windows Hello for Business provides a convenient method for seamlessly accessing corporate resources on-premises and in the cloud.


![image](https://github.com/user-attachments/assets/b4e92fc4-71a8-4ad3-8724-59f22a4542f4)

The following steps show how the sign-in process works with Microsoft Entra ID:


![image](https://github.com/user-attachments/assets/965c5c3b-9704-4cab-9626-3b10b81583ed)

1) A user signs into Windows using biometric or PIN gesture. The gesture unlocks the Windows Hello for Business private key and is sent to the Cloud Authentication security support provider, referred to as the Cloud AP provider.

2) The Cloud AP provider requests a nonce (a random arbitrary number that can be used just once) from Microsoft Entra ID.

3) Microsoft Entra ID returns a nonce that's valid for 5 minutes.

4) The Cloud AP provider signs the nonce using the user's private key and returns the signed nonce to the Microsoft Entra ID.

5) Microsoft Entra ID validates the signed nonce using the user's securely registered public key against the nonce signature. Microsoft Entra ID validates the signature and then validates the returned signed nonce. When the nonce is validated, Microsoft Entra ID creates a primary refresh token (PRT) with session key that is encrypted to the device's transport key and returns it to the Cloud AP provider. The Cloud AP provider receives the encrypted PRT with session key.

6) The Cloud AP provider uses the device's private transport key to decrypt the session key and protects the session key using the device's Trusted Platform Module (TPM).

7) The Cloud AP provider returns a successful authentication response to Windows. The user is then able to access Windows as well as cloud and on-premises applications without the need to authenticate again (SSO).

## Microsoft Authenticator

You can also allow your employee's phone to become a passwordless authentication method. You may already be using the Authenticator app as a convenient multifactor authentication option in addition to a password. You can also use the Authenticator App as a passwordless option.


![image](https://github.com/user-attachments/assets/d4d843df-915c-47e0-a165-f22a1064d046)

The Authenticator App turns any iOS or Android phone into a strong, passwordless credential. Users can sign in to any platform or browser by getting a notification to their phone, matching a number displayed on the screen to the one on their phone, and then using their biometric (touch or face) or PIN to confirm.

Passwordless authentication using the Authenticator app follows the same basic pattern as Windows Hello for Business. It's a little more complicated as the user needs to be identified so that Microsoft Entra ID can find the Authenticator app version being used:


![image](https://github.com/user-attachments/assets/71c2498f-00d0-4490-9d8e-8467f1361683)

1) The user enters their username.

2) Microsoft Entra ID detects that the user has a strong credential and starts the Strong Credential flow.

3) A notification is sent to the app via Apple Push Notification Service (APNS) on iOS devices, or via Firebase Cloud Messaging (FCM) on Android devices.

4) The user receives the push notification and opens the app.

5) The app calls Microsoft Entra ID and receives a proof-of-presence challenge and nonce.

6) The user completes the challenge by entering their biometric or PIN to unlock private key.

7) The nonce is signed with the private key and sent back to Microsoft Entra ID.

8) Microsoft Entra ID performs public/private key validation and returns a token.

## Passkeys (FIDO2)

The FIDO (Fast IDentity Online) Alliance helps to promote open authentication standards and reduce the use of passwords as a form of authentication. FIDO2 is the latest standard that incorporates the web authentication (WebAuthn) standard.

FIDO2 security keys are an unphishable standards-based passwordless authentication method that can come in any form factor. Fast Identity Online (FIDO) is an open standard for passwordless authentication. FIDO allows users and organizations to leverage the standard to sign in to their resources without a username or password using an external security key or a platform key built into a device.

Users can register and then select a FIDO2 security key at the sign-in interface as their main means of authentication. These FIDO2 security keys are typically USB devices, but could also use Bluetooth or NFC. With a hardware device that handles the authentication, the security of an account is increased as there's no password that could be exposed or guessed.

FIDO2 security keys can be used to sign in to their Microsoft Entra ID or Microsoft Entra hybrid joined Windows 10 devices and get single-sign on to their cloud and on-premises resources. Users can also sign in to supported browsers. FIDO2 security keys are a great option for enterprises who are very security sensitive or have scenarios or employees who aren't willing or able to use their phone as a second factor.

#### NOTE: If you purchase and plan to use NFC-based security keys, you need a supported NFC reader for the security key. The NFC reader isn't an Azure requirement or limitation. Check with the vendor for your NFC-based security key for a list of supported NFC readers.

![image](https://github.com/user-attachments/assets/3269eedb-51ca-49f6-a1a3-2d89ca36029e)

The following process is used when a user signs in with a FIDO2 security key:


![image](https://github.com/user-attachments/assets/ae2a1154-dcdc-416e-b3fb-e07ed57ab429)

1) The user plugs the FIDO2 security key into their computer.

2) Windows detects the FIDO2 security key.

3) Windows sends an authentication request.

4) Microsoft Entra ID sends back a nonce.

5) The user completes their gesture to unlock the private key stored in the FIDO2 security key's secure enclave.

6) The FIDO2 security key signs the nonce with the private key.

7) The primary refresh token (PRT) token request with signed nonce is sent to Microsoft Entra ID.

8) Microsoft Entra ID verifies the signed nonce using the FIDO2 public key.

9) Microsoft Entra ID returns PRT to enable access to on-premises resources.

## Certificate-based Authentication

Microsoft Entra certificate-based authentication (CBA) enables customers to allow or require users to authenticate directly with X.509 certificates against their Microsoft Entra ID for applications and browser sign-in. CBA enables customers to adopt phishing-resistant authentication and sign in with an X.509 certificate against their Public Key Infrastructure (PKI).

### Benefits

| Benefits                  | Description |
|---------------------------|-------------|
| **Great user experience**  | - Users who need certificate-based authentication can now directly authenticate against Microsoft Entra ID and not have to invest in federated AD FS. <br> - Portal UI enables users to easily configure how to map certificate fields to a user object attribute to look up the user in the tenant (certificate username bindings). <br> - Portal UI to configure authentication policies to help determine which certificates are single-factor versus multifactor. |
| **Easy to deploy and administer** | - Microsoft Entra CBA is a free feature, and you don't need any paid editions of Microsoft Entra ID to use it. <br> - No need for complex on-premises deployments or network configuration. <br> - Directly authenticate against Microsoft Entra ID. |
| **Secure** | - On-premises passwords don't need to be stored in the cloud in any form. <br> - Protects your user accounts by working seamlessly with Microsoft Entra Conditional Access policies, including Phishing-Resistant multifactor authentication (MFA requires licensed edition) and blocking legacy authentication. <br> - Strong authentication support where users can define authentication policies through the certificate fields, such as issuer or policy OID (object identifiers), to determine which certificates qualify as single-factor versus multifactor. <br> - The feature works seamlessly with Conditional Access features and authentication strength capability to enforce MFA to help secure your users. |

### Supported Scenarios

The following scenarios are supported:

1) User sign-ins to web browser-based applications on all platforms.

2) User sign-ins to Office mobile apps on iOS/Android platforms as well as Office native apps in Windows, including Outlook, OneDrive, and so on.

3) User sign-ins on mobile native browsers.

4) Support for granular authentication rules for multifactor authentication by using the certificate issuer Subject and policy OIDs.

5) Configuring certificate-to-user account bindings by using any of the certificate fields:

 - Subject Alternate Name (SAN) PrincipalName and SAN RFC822Name.

 - Subject Key Identifier (SKI) and SHA1PublicKey.

6) Configuring certificate-to-user account bindings by using any of the user object attributes:

 - User Principal Name

 - onPremisesUserPrincipalName

 - CertificateUserIds

### Unsupported scenarios

We recommend no more than 20 sets of keys for each passwordless method for any user account. As more keys are added, the user object size increases, and you may notice degradation for some operations. In that case, you should remove unnecessary keys.

When you use PowerShell to create a CSV file with all of the existing keys, carefully identify the keys that you need to keep, and remove those rows from the CSV. Then use the modified CSV with PowerShell to delete the remaining keys to bring the account key count under the limit.

It is safe to delete any key reported as "Orphaned"="True" in the CSV. An orphaned key is one for a device that is not longer registered in Microsoft Entra ID. If removing all Orphans still doesn't bring the User account below the limit it is necessary to look at the "DeviceId" and "CreationTime" columns to identify which keys to target for deletion. Be careful to remove any row in the CSV for keys you want to keep. Keys for any DeviceID corresponding to devices the user actively uses should be removed from the CSV before the deletion step.

