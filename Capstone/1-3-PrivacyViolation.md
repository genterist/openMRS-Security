## 1-3 PRIVACY VIOLATION

### Affected module : Whole OpenMRS System

### Vulnerability Description
Mishandling private information, such as user passwords or private information, can compromise user privacy, and is often illegal. Privacy violations occur when users' private information enters the program, or the data is written to an external location.

For this vulnerability, the method *authenticate()* in *Context.java*:287 mishandles confidential information. More specifically, the password enters the program. Furthermore, the statement `log.debug("Authenticating with username: " + username);` in *authenticate()* will display the username in log when debug is enabled. From a security perspective, system should log all important operations so that any anomalous activity can later be identified. However, when private data is involved, this practice can in fact create risk.

### Business impact
This vulnerability would allow attackers access to personal information, sensitive data and system functionabilities. The leakage of personal information will cause a financial loss to employee and patients of hospitals using openMRS system. As a consequence, the reputation of the hospital and openMRS team will also be heavily damaged. The hospital and the openMRS team may even face a charge or financial punishment to compensate the loss of patients and employees.

### Consequences
The application may reveal system data, personal information or debugging information by raising exceptions or generating error messages. Leakage of sensitive data through an output stream or logging function can allow attackers to gain knowledge about the application and craft specialized attacks on the it. Once the attackers successfully take advantage of this vulnerability, they can get the username and password of users. After they log in as a user, they can do whatever they want, such as stealing personal information, or even breaking the system.

### Mitigation

One potential fix for this problem is minimizing the exposure of sensitive data and encrypting them if they are needed. Make sure the source code of the application cannot be decompiled and interpolated by others.  Sanitize all messages, removing any unnecessary sensitive information. Ensure that debugging, error messages, and exceptions are only visible to developer.

For this vulnerability, we proposed a code fix shown below:

**Original code**

![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix7.png)
<br/>

**Modified code**

![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix8.png)


