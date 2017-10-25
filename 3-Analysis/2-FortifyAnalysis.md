## Static analysis with Fortify ##

### Overview ###

In this part we list 10 security vulnerabilities in OpenMRS and suggest potential fix for each. The prioritization is based on the impact and severity of each vulnerability. The vulnerabilities is prioritized based on its risk, which is **Risk = Impact · Likelihood**.

### Static Analysis ###

#### 1. SQL Injection ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | On line 164 of *MigrateAllergiesChangeSet.java*, the method *getConceptByGlobalProperty()* invokes a SQL query built using input coming from an untrusted source. This call could allow an attacker to modify the statement's meaning or to execute arbitrary SQL commands. |
| **Potential Fix** | 1. A common mistake is to use parameterized SQL statements that are constructed by concatenating user-controlled strings. Of course, this defeats the purpose of using parameterized SQL statements. If you are not certain that the strings used to form parameterized statements are constants controlled by the application, do not assume that they are safe because they are not being executed directly as SQL strings. Thoroughly investigate all uses of user-controlled strings in SQL statements and verify that none can be used to modify the meaning of the query. <br>2. A number of modern web frameworks provide mechanisms for performing validation of user input. Struts and Spring MVC are among them. To highlight the unvalidated sources of input, the Fortify Secure Coding Rulepacks dynamically re-prioritize the issues reported by Fortify Static Code Analyzer by lowering their probability of exploit and providing pointers to the supporting evidence whenever the framework validation mechanism is in use. We refer to this feature as Context-Sensitive Ranking. To further assist the Fortify user with the auditing process, the Fortify Software Security Research group makes available the Data Validation project template that groups the issues into folders based on the validation mechanism applied to their source of input. | 
| **Severity**: | 4.0 |
| **Confidence** | 5.0 |
| **Impact** | 5.0 |
| **Likelihood** | 5.0 |
| **Risk** | 25.0 |


#### 2. Command Injection ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | The method *execMysqlCmd()* in *MigrateDataSet.java*:187 calls *exec()* with a command built from untrusted data. This call can cause the program to execute malicious commands on behalf of an attacker. |
| **Potential Fix** | 1. A number of modern web frameworks provide mechanisms for performing validation of user input. Struts and Spring MVC are among them. To highlight the unvalidated sources of input, the Fortify Secure Coding Rulepacks dynamically re-prioritize the issues reported by Fortify Static Code Analyzer by lowering their probability of exploit and providing pointers to the supporting evidence whenever the framework validation mechanism is in use. We refer to this feature as Context-Sensitive Ranking. To further assist the Fortify user with the auditing process, the Fortify Software Security Research group makes available the Data Validation project template that groups the issues into folders based on the validation mechanism applied to their source of input. <br>2. Fortify RTA adds protection against this category. | 
| **Severity**: | 4.0 |
| **Confidence** | 5.0 |
| **Impact** | 5.0 |
| **Likelihood** | 3.2 |
| **Risk** | 16.0 |


#### 3. Privacy Violation ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | The method *authenticate()* in Context.java:287 mishandles confidential information, which can compromise user privacy and is often illegal. More specifically, the statement `log.debug("Authenticating with username: " + username);` in *authenticate()* will display the username in log when debug is enabled. |
| **Potential Fix** | 1. As part of any thorough audit for privacy violations, ensure that custom rules have been written to identify all sources of private or otherwise sensitive information entering the program. Most sources of private data cannot be identified automatically. Without custom rules, your check for privacy violations is likely to be substantially incomplete. <br>2. The Fortify Java Annotations FortifyPassword, FortifyNotPassword, FortifyPrivate and FortifyNotPrivate can be used to indicate which fields and variables represent passwords and private data. <br>3. A number of modern web frameworks provide mechanisms for performing validation of user input. Struts and Spring MVC are among them. To highlight the unvalidated sources of input, the Fortify Secure Coding Rulepacks dynamically re-prioritize the issues reported by Fortify Static Code Analyzer by lowering their probability of exploit and providing pointers to the supporting evidence whenever the framework validation mechanism is in use. We refer to this feature as Context-Sensitive Ranking. To further assist the Fortify user with the auditing process, the Fortify Software Security Research group makes available the Data Validation project template that groups the issues into folders based on the validation mechanism applied to their source of input. | 
| **Severity**: | 3.0 |
| **Confidence** | 5.0 |
| **Impact** | 4.0 |
| **Likelihood** | 2.8 |
| **Risk** | 11.2 |


#### 4. Password in Configuration File ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | In *liquibase-core-data.xml*:5, the password is stored as plaintext in the configuration file. Storing a plaintext password in a configuration file may result in a system compromise. |
| **Potential Fix** | 1. Fortify Static Code Analyzer searches configuration files for common names used for password properties. Audit these issues by verifying that the flagged entry is used as a password and that the password entry contains plaintext.<br>2. If the entry in the configuration file is a default password, require that it be changed in addition to requiring that it be obfuscated in the configuration file. | 
| **Severity**: | 4.0 |
| **Confidence** | 5.0 |
| **Impact** | 4.0 |
| **Likelihood** | 2.4 |
| **Risk** | 9.6 |


#### 5. Path Manipulation ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | Attackers are able to control the file system path argument to *File()* at *AbstractHandler.java* line 169, which allows them to access or modify otherwise protected files. |
| **Potential Fix** | 1. If the program is performing input validation, satisfy yourself that the validation is correct, and use the Fortify Custom Rules Editor to create a cleanse rule for the validation routine. <br>2. Implementation of an effective blacklist is notoriously difficult. One should be skeptical if validation logic requires blacklisting. Consider different types of input encoding and different sets of meta-characters that might have special meaning when interpreted by different operating systems, databases, or other resources. Determine whether or not the blacklist can be updated easily, correctly, and completely if these requirements ever change. <br>3. A number of modern web frameworks provide mechanisms for performing validation of user input. Struts and Spring MVC are among them. To highlight the unvalidated sources of input, the Fortify Secure Coding Rulepacks dynamically re-prioritize the issues reported by Fortify Static Code Analyzer by lowering their probability of exploit and providing pointers to the supporting evidence whenever the framework validation mechanism is in use. We refer to this feature as Context-Sensitive Ranking. To further assist the Fortify user with the auditing process, the Fortify Software Security Research group makes available the Data Validation project template that groups the issues into folders based on the validation mechanism applied to their source of input.| 
| **Severity**: | 3.0 |
| **Confidence** | 4.61 |
| **Impact** | 3.0 |
| **Likelihood** | 2.95 |
| **Risk** | 8.85 |


#### 6.Singleton Member ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | The class *AdministrationServiceImpl* is a singleton, so the member field *globalLocaleList* is shared between users. The result is that one user could see another user's data. |
| **Potential Fix** | 1. Do not use Servlet member fields for anything but constants. (i.e. make all member fields static final). 2. Developers are often tempted to use Servlet member fields for user data when they need to transport data from one region of code to another. If this is your aim, consider declaring a separate class and using the Servlet only to "wrap" this new class. | 
| **Severity**: | 4.0 |
| **Confidence** | 5.0 |
| **Impact** | 4.0 |
| **Likelihood** | 2.0 |
| **Risk** | 8.0 |


#### 7. Server-Side Request Forgery ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | The function *openConnection()* on line 720 initiates a network connection to a third-party system using user-controlled data for resource URI. An attacker may leverage this vulnerability to send a request on behalf of the application server since the request will originate from the application server internal IP. |
| **Potential Fix** | 1. Do not establish network connections based on user-controlled data and ensure that the request is being sent to the expected destination. If user data is necessary to build the destination URI, use a level of indirection: create a list of legitimate resource names that a user is allowed to specify, and only allow the user to select from the list. With this approach the input provided by the user is never used directly to specify the resource name.<br>2. In some situations this approach is impractical because the set of legitimate resource names is too large or too hard to keep track of. Programmers often resort to blacklisting in these situations. Blacklisting selectively rejects or escapes potentially dangerous characters before using the input. However, any such list of unsafe characters is likely to be incomplete and will almost certainly become out of date. A better approach is to create a whitelist of characters that are allowed to appear in the resource name and accept input composed exclusively of characters in the approved set. | 
| **Severity**: | 3.0 |
| **Confidence** | 5.0 |
| **Impact** | 3.0 |
| **Likelihood** | 2.4 |
| **Risk** | 7.2 |


#### 8. Hardcoded Encryption Key ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | In *OpenmrsConstants.java*:532, the encryption key is hardcoded in the program. Hardcoded encryption keys may compromise system security in a way that cannot be easily remedied. |
| **Potential Fix** | 1. Encryption keys should never be hardcoded and should be obfuscated and managed in an external source. Storing encryption keys in plaintext anywhere on the system allows anyone with sufficient permissions to read and potentially misuse the encryption key. | 
| **Severity**: | 3.0 |
| **Confidence** | 5.0 |
| **Impact** | 3.0 |
| **Likelihood** | 2.4 |
| **Risk** | 7.2 |


#### 9. Denial of Service: Regular Expression ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | In *HibernatePatientDAO.java*:772, untrusted data is passed to the application and used as a regular expression. This can cause the thread to over-consume CPU resources. |
| **Potential Fix** | 1. Do not allow untrusted data to be used as regular expression patterns. | 
| **Severity**: | 4.0 |
| **Confidence** | 4.43 |
| **Impact** | 3.0 |
| **Likelihood** | 2.13 |
| **Risk** | 6.39 |


#### 10. Log Forging ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | The method *becomeUser()* in Context.java writes unvalidated user input to the log on line 328. An attacker could take advantage of this behavior to forge log entries or inject malicious content into the log. |
| **Potential Fix** | 1. Many logging operations are created only for the purpose of debugging a program during development and testing. In our experience, debugging will be enabled, either accidentally or purposefully, in production at some point. Do not excuse log forging vulnerabilities simply because a programmer says "I don't have any plans to turn that on in production". <br>2. A number of modern web frameworks provide mechanisms for performing validation of user input. Struts and Spring MVC are among them. To highlight the unvalidated sources of input, the Fortify Secure Coding Rulepacks dynamically re-prioritize the issues reported by Fortify Static Code Analyzer by lowering their probability of exploit and providing pointers to the supporting evidence whenever the framework validation mechanism is in use. We refer to this feature as Context-Sensitive Ranking. To further assist the Fortify user with the auditing process, the Fortify Software Security Research group makes available the Data Validation project template that groups the issues into folders based on the validation mechanism applied to their source of input. | 
| **Severity**: | 3.0 |
| **Confidence** | 4.6 |
| **Impact** | 2.5 |
| **Likelihood** | 2.21 |
| **Risk** | 5.525 |
