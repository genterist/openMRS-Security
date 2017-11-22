## 1-4 PASSWORD IN CONFIGURATION FILE

### Affected module : Whole OpenMRS System

### Vulnerability Description

In *liquibase-core-data.xml*:5, the password is stored as plaintext in the configuration file.  Storing a password in plaintext may result in a system compromise. Password management issues occur when a password is stored in plaintext in an application's properties or configuration file. Storing a plaintext password in a configuration file allows anyone who can read the file access to the password-protected resource. 

### Business impact


### Consequences


### Mitigation
One potential fix for this problem is encrypting the password field or the whole configuration file, then the plaintext password will not be retrieved by attacker. Another potential fix is assigning access permission on the configuration file. So the plaintext password is not accessible to the attackers without permission.

#### Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix7.png)
<br/>

#### Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix8.png)

A programmer can attempt to remedy the password management problem by obscuring the password with an encoding function, such as base 64 encoding, but this effort does not adequately protect the password.

