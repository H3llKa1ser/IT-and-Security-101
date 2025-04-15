# Evaluate Windows Local Admin Password Solution (LAPS) solutions

Windows Local Administrator Password Solution (Windows LAPS) is a Windows feature that automatically manages and backs up the password of a local administrator account on your Microsoft Entra joined or Windows Server Active Directory-joined devices. You also can use Windows LAPS to automatically manage and back up the Directory Services Restore Mode (DSRM) account password on your Windows Server Active Directory domain controllers. An authorized administrator can retrieve the DSRM password and use it.

## Windows LAPS supported platforms

Windows LAPS is now available on the following OS platforms with the specified update or later installed:

1) Windows 11 22H2 - April 11 2023 Update

2) Windows 11 21H2 - April 11 2023 Update

3) Windows 10 - April 11 2023 Update

4) Windows Server 2022 - April 11 2023 Update

5) Windows Server 2019 - April 11 2023 Update

## Benefits of using Windows LAPS

Use Windows LAPS to regularly rotate and manage local administrator account passwords and get these benefits:

1) Protection against pass-the-hash and lateral-traversal attacks

2) Improved security for remote help desk scenarios

3) Ability to sign in to and recover devices that are otherwise inaccessible

4) A fine-grained security model (access control lists and optional password encryption) for securing passwords that are stored in Windows Server Active Directory

5) Support for the Entra role-based access control model for securing passwords that are stored in Microsoft Entra ID

## Key Windows LAPS scenarios

You can use Windows LAPS for several primary scenarios:

1) Back up local administrator account passwords to Microsoft Entra ID (for Microsoft Entra-joined devices)

2) Back up local administrator account passwords to Windows Server Active Directory (for Windows Server Active Directory-joined clients and servers)

3) Back up DSRM account passwords to Windows Server Active Directory (for Windows Server Active Directory domain controllers)

4) Back up local administrator account passwords to Windows Server Active Directory by using legacy Microsoft LAPS

In each scenario, you can apply different policy settings.

## Windows LAPS vs. legacy Microsoft LAPS

Windows LAPS inherits many design concepts from legacy Microsoft LAPS. If you're familiar with legacy Microsoft LAPS, many Windows LAPS features are familiar. A key difference is that Windows LAPS is an entirely separate implementation that's native to Windows. Windows LAPS also adds many features that aren't available in legacy Microsoft LAPS. You can use Windows LAPS to back up passwords to Azure Active Directory, encrypt passwords in Windows Server Active Directory, and store your password history.
