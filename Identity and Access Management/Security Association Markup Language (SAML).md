# Security Association Markup Language (SAML)

## Example

### 1) User tries to reach Atlassian application

### 2) SAML SSO Plugin generates SAML-Request (SSO)

### 3) SAML SSO Plugin redirects browser with SAML-Request to Identity Provider (SSO)

### 4) Identity provider pares SAML-Request, authenticates user 

### 5) Identity provider generates SAML-Response containing user information

### 6) Identity provider redirects browser with SAML-response to SAML-SSO Plugin

### 7) SAML SSO Plugin verifies SAML-Response (SSO)

### 8) SAML SSO Plugin creates or updates user if configured (SSO)

### 9) User is logged into the Atlassian application
