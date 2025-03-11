# New Technology LAN Manager (NTLM) Authentication

NTLM authentication is a family of authentication protocols that are encompassed in the Windows Msv1_0.dll. The NTLM authentication protocols include LAN Manager version 1 and 2, and NTLM version 1 and 2. The NTLM authentication protocols authenticate users and computers based on a challenge/response mechanism that proves to a server or domain controller that a user knows the password associated with an account. When the NTLM protocol is used, a resource server must take one of the following actions to verify the identity of a computer or user whenever a new access token is needed:

1) Contact a domain authentication service on the domain controller for the computer's or user's account domain, if the account is a domain account.

2) Look up the computer's or user's account in the local account database, if the account is a local account.

## Current Applications

NTLM authentication is still supported and must be used for Windows authentication with systems configured as a member of a workgroup. NTLM authentication is also used for local logon authentication on non-domain controllers. Kerberos version 5 authentication is the preferred authentication method for Active Directory environments, but a non-Microsoft or Microsoft application might still use NTLM.

Reducing the usage of the NTLM protocol in an IT environment requires both the knowledge of deployed application requirements on NTLM and the strategies and steps necessary to configure computing environments to use other protocols. New tools and settings have been added to help you discover how NTLM is used in order to selectively restrict NTLM traffic.

## New and changed functionality

There are no changes in functionality for NTLM for Windows Server.

## Removed or deprecated functionality

There is no removed or deprecated functionality for NTLM for Windows Server.

## Server Manager information

NTLM cannot be configured from Server Manager. You can use Security Policy settings or Group Policies to manage NTLM authentication usage between computer systems. In a domain, Kerberos is the default authentication protocol.

