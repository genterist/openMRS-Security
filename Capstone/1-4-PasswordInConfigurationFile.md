## 1-4 PASSWORD IN CONFIGURATION FILE

### Affected module : Whole OpenMRS System

### Vulnerability Description
Storing a password in plaintext may result in a system compromise. Password management issues occur when a password is stored in plaintext in an application's properties or configuration file. Storing a plaintext password in a configuration file allows anyone who can read the file access to the password-protected resource.

For this vulnerability, in *liquibase-core-data.xml*:5, the password is stored as plaintext in the configuration file.  

### Business impact
This vulnerability would allow attackers access to the password and the resources the password protects. There is possibility that the attacker could make the system out of service by some methods such as changing the password. As a consequence, this would cause a impediment for hospitals relying on the openMRS system. The hospitals would suffer a loss of money to ensure normal operations. The openMRS system would also suffer a loss of reputation.

### Consequences
Once the attackers successfully take advantage of this vulnerability, the access control of openMRS system will be violated. This can result in compromise of the system for which the password is used. An attacker could gain access to this file and learn the stored password or even change the password to one of their choosing. Also, the attackers could access to the resources the password protects and then cause damage to the system. 

### Mitigation

To solve the problem, one efficient method is avoiding storing passwords in easily accessible locations. However, removing the fields in configuration file may need enormous architecture change and even break the system. So, another potential mitigation method for this problem is encrypting the password field or the whole configuration file with cryptographic hashes Then the plaintext password will not be retrieved by attacker. Also we can assign access permission on the configuration file. So the plaintext password is not accessible to the attackers without permission.

For this vulnerability, we proposed a code fix shown below:

**Original code:**

![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix7.png)


**Modified code:** 

![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix8.png)




