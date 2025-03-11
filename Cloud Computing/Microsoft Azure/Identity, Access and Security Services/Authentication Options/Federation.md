# Federation

Federation is a collection of domains that have established trust. The level of trust may vary, but typically includes authentication and almost always includes authorization. A typical federation might include a number of organizations that have established trust for shared access to a set of resources.

You can federate your on-premises environment with Microsoft Entra ID and use this federation for authentication and authorization. This sign-in method ensures that all user authentication occurs on-premises. This method allows administrators to implement more rigorous levels of access control. Federation with AD FS and PingFederate is available.

### TIP: If you decide to use Federation with Active Directory Federation Services (AD FS), you can optionally set up password hash synchronization as a backup in case your AD FS infrastructure fails.

Microsoft Entra Connect lets you configure federation with on-premises Active Directory Federation Services (AD FS) and Microsoft Entra ID. With federation sign-in, you can enable users to sign in to Microsoft Entra ID-based services with their on-premises passwords--and, while on the corporate network, without having to enter their passwords again. By using the federation option with AD FS, you can deploy a new installation of AD FS, or you can specify an existing installation in a Windows Server 2012 R2 farm.

