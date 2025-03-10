# Decision Tree Diagram for Auth Method

![image](https://github.com/user-attachments/assets/5dbb260b-c1f6-44ed-9671-33803819382e)

### Details on decision questions:

1) Microsoft Entra ID can handle sign-in for users without relying on on-premises components to verify passwords.

2) Microsoft Entra ID can hand off user sign-in to a trusted authentication provider such as Microsoft's AD FS.

3) If you need to apply, user-level Active Directory security policies such as account expired, disabled account, password expired, account locked out, and sign-in hours on each user sign-in, Microsoft Entra ID requires some on-premises components.

4) Sign-in features not natively supported by Microsoft Entra ID:

 - Sign-in using third-party authentication solution.

 - Multi-site on-premises authentication solution.

5) Microsoft Entra ID Protection requires Password Hash Sync regardless of which sign-in method you choose, to provide the Users with leaked credentials report. Organizations can fail over to Password Hash Sync if their primary sign-in method fails and it was configured before the failure event.

#### NOTE: Microsoft Entra ID Protection requires Microsoft Entra ID P2 licenses.

