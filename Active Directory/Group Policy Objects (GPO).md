# Group Policy Objects (GPO)

### To configure GPOs, we use the Group Policy Management tool.

### GPOs are a collection of settings that can be applied to OUs.

# GPO Distribution

### GPOs are distributed to the network via a network share called SYSVOL which is stoerd in the DC. All users in a domain have access to this share to sync their GPOs periodically. 

### The SYSVOL share points to: C:\Windows\SYSVOL\sysvol\

### Once a change has been made to any GPOs, it might take up to 2 hrs for computers to catchup.

## PS C:\> gpupdate /force (Force updates GPOs immediately!)
