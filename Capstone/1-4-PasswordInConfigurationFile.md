## 1-4 PASSWORD IN CONFIGURATION FILE

### Affected module : OpenMRS login

### Bug Description

In *liquibase-core-data.xml*:5, the password is stored as plaintext in the configuration file. Storing a plaintext password in a configuration file may result in a system compromise.

### Business impact
one paragraph on the negative consequences of the vulnerability to the organization using OpenMRS

### Result
one paragraph summarizing the consequences of the vulnerability

### Mitigation
One potential fix for this problem is encrypting the password field or the whole configuration file, then the plaintext password will not be retrieved by attacker. Another potential fix is assigning access permission on the configuration file. So the plaintext password is not accessible to the attackers without permission.

#### Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix7.png)
<br/>

#### Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix8.png)
<br/>
Follow recommendations at https://wiki.openmrs.org/display/docs/Security+and+Encryption we encode the plain password using the built-in "encodeString" function. This change has to be made accross all authentication functions that output password into XML files.
