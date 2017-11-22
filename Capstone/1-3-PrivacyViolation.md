## 1-3 PRIVACY VIOLATION

### Affected module : Whole OpenMRS System

### Vulnerability Description
Mishandling private information, such as user passwords or private information, can compromise user privacy, and is often illegal. Privacy violations occur when users' private information enters the program, or the data is written to an external location.

For this vulnerability, the method *authenticate()* in *Context.java*:287 mishandles confidential information. More specifically, the password enters the program. Furthermore, the statement `log.debug("Authenticating with username: " + username);` in *authenticate()* will display the username in log when debug is enabled.

### Business impact
Once the attacker successfully takes advantage of this vulnerability

### Consequences


### Mitigation
Phase: Architecture and Design
Avoid storing passwords in easily accessible locations.
Phase: Architecture and Design
Consider storing cryptographic hashes of passwords as an alternative to storing in plaintext

We proposed the short term fix and the long term fix.
The short term fix is to truncate the raw location ID string before converting it to integer to be used by other functions. This is one example of a possible fix

#### Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix7.png)
<br/>

#### Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix8.png)

One potential fix for this problem is minimizing the exposure of sensitive data and encrypting them if they are needed.  Making sure the source code of the application cannot be decompiled and interpolated by others.
