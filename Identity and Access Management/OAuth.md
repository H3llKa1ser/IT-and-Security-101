# Open Standard for Authorization (OAuth)

### OAuth has different intent

### Not designed for SSO

### Provides delegation of rights to applications

### In simplest terms, it means giving your access to someone you trust, so that they can perform the job on your brhalf 

### (E.g. Updating status across facebook, Instagram, twitter, etc with a single click)

### Could go to the sites manually, but easier to delegate access to an app that connects the above platforms

### Authenticate yourself to Facebook. Facebook provides a consent page stating you are about to give this app rights to update status on your behalf.

### If you agree, the app gets an opaque access token from Facebook, app stores that access token, send the status update with access token to Facebook.

### Facebook validates the access token (easy in this case as the token was issued by Facebook itself), and updates your status.
