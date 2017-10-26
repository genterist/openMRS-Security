## Static analysis with Fortify ##

### Overview ###

In this part we list 10 security vulnerabilities in OpenMRS and suggest potential fix for each. The prioritization is based on the impact and severity of each vulnerability. The vulnerabilities is prioritized from high to low based on its risk, which is **Risk = Impact · Likelihood**.

### Static Analysis ###

#### 1. SQL Injection ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | On line 164 of *MigrateAllergiesChangeSet.java*, the method *getConceptByGlobalProperty()* invokes a SQL query built using input coming from an untrusted source. This call could allow an attacker to modify the statement's meaning or to execute arbitrary SQL commands. |
| Potential Fix | 1. Replacing the query execution statement with parameterized SQL statements can enforce this behavior by disallowing data-directed context changes and avoiding nearly all SQL injection attacks. <br>2. Another potential fix is adopting modern web framework. A number of modern web frameworks provide mechanisms for performing validation of user input, like Struts and Spring MVC. But the cost of changing design or architecture of current application may be very high. | 
| Impact | 5.0 |
| Likelihood | 5.0 |
| **Risk** | 25.0 |


#### 2. Command Injection ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | The method *execMysqlCmd()* in *MigrateDataSet.java*:187 calls *exec()* with a command built from untrusted data. This call can cause the program to execute malicious commands on behalf of an attacker. |
| Potential Fix | 1.Building a filter / validation method that check the command before the command is executed by *execMysqlCmd()*. The input could be selected from a predetermined set of safe commands. <br>2. Another potential fix is adopting modern web framework. A number of modern web frameworks provide mechanisms for performing validation of user input, like Struts and Spring MVC. But the cost of changing design or architecture of current application may be very high. | 
| Impact | 5.0 |
| Likelihood | 3.2 |
| **Risk** | 16.0 |


#### 3. Privacy Violation ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | The method *authenticate()* in *Context.java*:287 mishandles confidential information, which can compromise user privacy and is often illegal. More specifically, the password enters the program, and the statement `log.debug("Authenticating with username: " + username);` in *authenticate()* will display the username in log when debug is enabled. |
| Potential Fix | 1. One potential fix for this problem is minimizing the exposure of sensitive data and encrypting them if they are needed. <br>2. Making sure the source code of the application cannot be decompiled and interpolated by others. | 
| Impact | 4.0 |
| Likelihood | 2.8 |
| **Risk** | 11.2 |


#### 4. Password in Configuration File ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | In *liquibase-core-data.xml*:5, the password is stored as plaintext in the configuration file. Storing a plaintext password in a configuration file may result in a system compromise. |
| Potential Fix | 1. One potential fix for this problem is encrypting the password field or the whole configuration file, then the plaintext password will not be retrieved by attacker.<br>2. Another potential fix is assigning access permission on the configuration file. So the plaintext password is not accessible to the attackers without permission. | 
| Impact | 4.0 |
| Likelihood | 2.4 |
| Risk | 9.6 |


#### 5. Path Manipulation ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | Attackers are able to control the file system path argument to *File()* at *AbstractHandler.java* line 169, which allows them to access or modify otherwise protected files. |
| Potential Fix | 1. If the program is performing input validation, satisfy yourself that the validation is correct, and use the Fortify Custom Rules Editor to create a cleanse rule for the validation routine. <br>2. Implementation of an effective blacklist is notoriously difficult. One should be skeptical if validation logic requires blacklisting. Consider different types of input encoding and different sets of meta-characters that might have special meaning when interpreted by different operating systems, databases, or other resources. Determine whether or not the blacklist can be updated easily, correctly, and completely if these requirements ever change. <br>3. Another potential fix is adopting modern web framework. A number of modern web frameworks provide mechanisms for performing validation of user input, like Struts and Spring MVC. But the cost of changing design or architecture of current application may be very high.| 
| Impact | 3.0 |
| Likelihood | 2.95 |
| **Risk** | 8.85 |


#### 6.Singleton Member ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | The class *AdministrationServiceImpl* is a singleton, so the member field *globalLocaleList* is shared between users. The result is that one user could see another user's data. |
| Potential Fix | 1. For this problem, one potential fix is declaring a separate class and using the Servlet only to wrap the new class. <br>2.Changing the design of AdministrationServiceImpl and placing the member field *globalLocaleList* into another class. | 
| Impact | 4.0 |
| Likelihood | 2.0 |
| **Risk** | 8.0 |


#### 7. Server-Side Request Forgery ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | The function *openConnection()* on line 720 initiates a network connection to a third-party system using user-controlled data for resource URI. An attacker may leverage this vulnerability to send a request on behalf of the application server since the request will originate from the application server internal IP. |
| **Potential Fix** | 1. Do not establish network connections based on user-controlled data and ensure that the request is being sent to the expected destination. If user data is necessary to build the destination URI, use a level of indirection: create a list of legitimate resource names that a user is allowed to specify, and only allow the user to select from the list. With this approach the input provided by the user is never used directly to specify the resource name.<br>2. In some situations this approach is impractical because the set of legitimate resource names is too large or too hard to keep track of. Programmers often resort to blacklisting in these situations. Blacklisting selectively rejects or escapes potentially dangerous characters before using the input. However, any such list of unsafe characters is likely to be incomplete and will almost certainly become out of date. A better approach is to create a whitelist of characters that are allowed to appear in the resource name and accept input composed exclusively of characters in the approved set. | 
| Impact | 3.0 |
| Likelihood | 2.4 |
| **Risk** | 7.2 |


#### 8. Hardcoded Encryption Key ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | In *OpenmrsConstants.java*:532, the encryption key is hardcoded in the program. Hardcoded encryption keys may compromise system security in a way that cannot be easily remedied. |
| Potential Fix | 1. Encryption keys should never be hardcoded and should be obfuscated and managed in an external source. Storing encryption keys in plaintext anywhere on the system allows anyone with sufficient permissions to read and potentially misuse the encryption key. | 
| Impact | 3.0 |
| Likelihood | 2.4 |
| **Risk** | 7.2 |


#### 9. Denial of Service: Regular Expression ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | In *HibernatePatientDAO.java*:772, untrusted data is passed to the application and used as a regular expression. This can cause the thread to over-consume CPU resources. |
| Potential Fix | 1. Do not allow untrusted data to be used as regular expression patterns. | 
| Impact | 3.0 |
| Likelihood | 2.13 |
| **Risk** | 6.39 |


#### 10. Log Forging ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | The method *becomeUser()* in Context.java writes unvalidated user input to the log on line 328. An attacker could take advantage of this behavior to forge log entries or inject malicious content into the log. |
| Potential Fix | 1. Many logging operations are created only for the purpose of debugging a program during development and testing. In our experience, debugging will be enabled, either accidentally or purposefully, in production at some point. Do not excuse log forging vulnerabilities simply because a programmer says "I don't have any plans to turn that on in production". <br>2. One potential fix is adopting modern web framework. A number of modern web frameworks provide mechanisms for performing validation of user input, like Struts and Spring MVC. But the cost of changing design or architecture of current application may be very high. | 
| Impact | 2.5 |
| Likelihood | 2.21 |
| **Risk** | 5.525 |
