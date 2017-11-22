## 1-3 PRIVACY VIOLATION

### Affected module : OpenMRS login

### Bug Description
The method *authenticate()* in *Context.java*:287 mishandles confidential information, which can compromise user privacy and is often illegal. More specifically, the password enters the program, and the statement `log.debug("Authenticating with username: " + username);` in *authenticate()* will display the username in log when debug is enabled.

### Business impact
one paragraph on the negative consequences of the vulnerability to the organization using OpenMRS

### Result
one paragraph summarizing the consequences of the vulnerability

### Mitigation
One potential fix for this problem is minimizing the exposure of sensitive data and encrypting them if they are needed.  Making sure the source code of the application cannot be decompiled and interpolated by others.

#### Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix7.png)
<br/>

#### Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix8.png)
<br/>
Follow recommendations at https://wiki.openmrs.org/display/docs/Security+and+Encryption we encode the plain password using the built-in "encodeString" function. This change has to be made accross all authentication functions that use plain password as input.