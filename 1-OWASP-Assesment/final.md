# A10 - API - User object - Unvalidated Redirects and Forwards
### Priority : medium
### Test status : PASSED
`DESIGNER : Fuxing Luan` <br/>

### * Description
#### Name of module : OpenMRS API - "User" object
This test determines the level of OpenMRS API User object's protection against unauthorized access.

### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OpenMRS Webservice API installed
5. Curl installed (optional)

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OpenMRS webservice API (https://modules.openmrs.org/#/show/153/webservices-rest)

### * Test Data
http://localhost:8081/openmrs- standalone/coreapps/activeVisits.page?app=www.google.com

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. 
2. direct to the url in the test data

### * Expected results
1. The page should be redirected to “www.google.com”

### * Actual results
1. The page was redirected to “www.google.com”
# A10 - API - User object - TEST FOR AUTHENTICATION
### Priority : medium
### Test status : PASSED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 09SEP2017` <br/>
`EXECUTED ON : 09SEP2017` <br/>

### * Description
#### Name of module : OpenMRS API - "User" object
This test determines the level of OpenMRS API User object's protection against unauthorized access.

### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OpenMRS Webservice API installed
5. Curl installed (optional)

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OpenMRS webservice API (https://modules.openmrs.org/#/show/153/webservices-rest)

### * Test Data
http://localhost:8081/openmrs-standalone/ws/rest/v1/user/
and/or
curl -X GET --header 'Accept: application/json' 'http://localhost:8081/openmrs-standalone/ws/rest/v1/user'  (optional)

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.
2. Open a web browser. Make sure no user was logged in, and paste this following url in : http://localhost:8081/openmrs-standalone/ws/rest/v1/user/
3. This step is optional. Open a command line, make sure Curl was installed, paste and run this command: curl -X GET --header 'Accept: application/json' 'http://localhost:8081/openmrs-standalone/ws/rest/v1/user'
4. In either case, observe to see if there is a prompt for inputting username/password. If there is a prompt, please put in wrong username/password and observe the result.

### * Expected results
1. For test step 2, web browser should load an XML file. Around line 15, you will see "User is not logged in [Privileges required: Get Users]" and the rest of the file contains troubleshooting information regarding the api.
2. For test step 3, you should be able to see the similar message and/or a 401 message, saying "USer not logged in"

### * Post-condition
Webservice API is still up, available to serve further requests.

### * Actual results
1. Used the browser test method and received and XML with "User is not logged in [Privileges required: Get Users]"

### * NOTES:
* OpenMRS API documentation together with examples can be found at http://localhost:8081/openmrs-standalone/module/webservices/rest/apiDocs.htm (logged in as admin first)
You can expand the objects and click "try it out" to get sample codes.
* You can install the OpenMRS webservice API by downloading it from https://modules.openmrs.org/#/show/153/webservices-rest and then move the downloaded file to [download folder]\referenceapplication-standalone-2.6.0\appdata\modules
* Contact tam.nguyen@ncsu.edu if you have problems following instructions in this test case.# [A1 - Injection] [ Drop Table ]
`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [09/09/2017]`

### Name of module : [  ]

### Priority : [high]

### Test Description
Injection attacks occur when unvalidated input is embedded in an instruction stream and cannot be distinguished from valid instructions.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
1. Username: `nurse`
2. Password: `Nurse123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Input "DROP TABLE Patients" in the search field

### * Expected results
1. No result will be shown

### * Actual results
 No result showed

### Test status : [ pass ]
# [A1 - Injection] [ Tautology ]
`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [09/09/2017]`

### Name of module : [  ]

### Priority : [high]

### Test Description
Injection attacks occur when unvalidated input is embedded in an instruction stream and cannot be distinguished from valid instructions.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
1. Username: ’ OR ‘1’ = ‘1 
2. Password: ’ OR ‘1’ = ‘1 

### * Test steps
1. Start local openMRS and 
2. Log in with the username and account

### * Expected results
1. Fail to login

### * Actual results
Login Failed

### Test status : [ pass ]
# [A2 - BAC] [ Exposed Session IDs ]
`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [09/09/2017]`

### Name of module : [  ]

### Priority : [high]

### Test Description : Broken Access Control 
Access control, sometimes called authorization, is how a web application grants access to content and functions to some users and not others. These checks are performed after authentication, and govern what 'authorized' users are allowed to do

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
1. Username: `nurse`
2. Password: `Nurse123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click all kinds of links and see the urls

### * Expected results
1. No session infomation will be exposed in the urls

### * Actual results
No session infomation exposed

### Test status : [ pass ]
# [A2 - BAC] [ Session Time Outs ]
`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [09/09/2017]`

### Name of module : [  ]

### Priority : [high]

### Test Description : Broken Access Control 
Access control, sometimes called authorization, is how a web application grants access to content and functions to some users and not others. These checks are performed after authentication, and govern what 'authorized' users are allowed to do

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
1. Username: `nurse`
2. Password: `Nurse123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Close browser
3. Reopen browser and visit the website again

### * Expected results
1. Login will be required

### * Actual results
Login is required

### Test status : [ pass ]
# [A3 - XSS] [ Detecting Reflected XSS ]
`DESIGNER : [Xiangqing Ding]`
`UPDATED ON : [09/09/2017]`

### Name of module : [ Find Patient Record ]

### Priority : [high]

### Test Description
XSS attacks are essentially code injection attacks into the various interpreters in the browser. This test case is trying to detect if script can be integrated in HTML and executed.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
1. Username: `nurse`
2. Password: `Nurse123`
3. Scripts: `<script>alert("Attacked")</script>` and `%3cscript%3ealert("Attacked")%3cscript%3e`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Input scripts in the search field and search

### * Expected results
1. The script is not accepted
2. The input is accepted but changed to valid form
3. The script is accepted but not executed

### * Actual results
The script doesn't work

### Test status : [ pass ]# [ A3 - XSS ] [ Detecting Stored XSS ]
`DESIGNER : [Xiangqing Ding]`
`UPDATED ON : [09/09/2017]`

### Name of module : [ Allergy page ]

### Priority : [high]

### Test Description


XSS attacks are essentially code injection attacks into the various interpreters in the browser. This test case is trying to see if script can be stored and executed in the allergy page.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
1. Username: `nurse`
2. Password: `Nurse123`
3. Script: `<script>alert("Attacked")</script>`

### * Test steps
1. Start openMRS and log in with username and password provided
2. Click “Find Patient Record” button in the main page
3. Search one of the patient (e.g. Christopher Allen) and go to the patient page by clicking the entry
4. In the patient page, find ALLERGIES column and click the edit button
5. In the allergy page, click “Add New Allergy” button to add a new allergy
6. In the “comment” field, add the script. Other field can be filled with own choice. After that, save the allergy.
7. Go to the allergy page again to see if there is a popup with message “Attacked”

### * Expected results
1. The script is not accepted
2. The script is accepted but changed to valid form
3. The script is accepted but not executed

### * Actual results
The script is accepted but doesn’t work

### Test status : [ pass ]# [ A4 - BAC ] [ Non-admin account access to admin function ]
`DESIGNER : [Xiangqing Ding]`
`UPDATED ON : [09/09/2017]`

### Name of module : [ System Administration ]

### Priority : [high]

### Test Description
This test case is designed to test whether a non-admin user can access to admin functions

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
1. Username: `nurse`
2. Password: `Nurse123`

### * Test steps
1. Start local openMRS and log in with username and password
2. Replace the `/referenceapplication/home.page` in the URL with `/coreapps/systemadministration/systemAdministration.page`
3. Direct the URL to see if the user can access to the system administration page

### * Expected results
User cannot access to system administration page while logging in as Nurse account (non-admin)

### * Actual results
The Nurse account can access to the administration page

### Test status : [ fail ]# [ A4 - BAC ] [ Unauthorized access to system ]
`DESIGNER : [Xiangqing Ding]`
`UPDATED ON : [09/09/2017]`

### Name of module : [ Main Page ]

### Priority : [high]

### Test Description
This test case is designed to test whether someone could access to the system without logging in

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
N/A

### * Test steps
1. Start local openMRS
2. Without logging in, put `http://localhost:8081/openmrs-standalone/referenceapplication/home.page` in the URL of browser.
3. Direct the URL to see if it can access to the system.

### * Expected results
User cannot access to the main page without logging in

### * Actual results
User cannot access to the main page without logging in

### Test status : [ pass ]# [A5 - Security Misconfiguration ] [ Default username and password]
### Test status : [ pass ]
`DESIGNER : [ZHUO LI]` <br/>
`UPDATED ON : [05SEP2017]` <br/>

### * Description

This test verified there is no default username and password which can bu used by hacker.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
Test username: admin

Test password: password

Test username: user

Test password: password

### * Test steps
1. Go to the home page
2. Try default user name and password such as admin

### * Expected results
There should be no default user name and password.

### * Actual results

![alt text](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Result/A5_001.PNG)
# [A5 - Security Misconfiguration ] [ DirectoryListing]
### Test status : [ pass ]
`DESIGNER : [ZHUO LI]` <br/>
`UPDATED ON : [05SEP2017]` <br/>

### * Description

This test verified the application will not list any directory when we only change the link.


### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
Test username: admin

Test password: Admin123

### * Test steps
1. Log in as admin
2. Change the link to directorylisting.(localhost://8081/openmrs-standalone/directorylisting)

### * Expected results
The application should not list any directory.

### * Actual results

![alt text](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Result/A5_002.PNG)
# [A6 - Sensitive Data Exposure ] [ Search History ]
### Test status : [ Failed ]
`DESIGNER : [ZHUO LI]` <br/>
`UPDATED ON : [05SEP2017]` <br/>

### * Description

This test verified the application will not list searching history when we exit the searching page.


### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
Test username: admin

Test password: Admin123

### * Test steps
1. Log in as admin and register two patients named “Frank” and “Fred”
2. Back to home page.
3. Click on search patient and right click "Frank".
4. Redo step 2-3 and search "Fred".
5. Check whether the source code remember admin’s behavior.

### * Expected results
There should be no information about Frank.

### * Actual results
![alt text](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Result/A6_002.PNG)
# [A6 - Sensitive Data Exposure ] [ Web Certification ]
### Test status : [ Failed ]
`DESIGNER : [ZHUO LI]` <br/>
`UPDATED ON : [05SEP2017]` <br/>

### * Description

This test verified the application need to certificate on every webpage.


### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally
2. Chrome or Firefox that can check security

### * Test Data
Test username: admin

Test password: Admin123

### * Test steps
1. Log in as admin
2. Test the certificate via Google chrome

### * Expected results
The web application should have certification on each available website.

### * Actual results

![alt text](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Result/A6_001.PNG)
# A7 - IAP - DETECTING LEADING SPACE ATTACK
### Priority : medium
### Test status : FAILED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 09SEP2017` <br/>
`EXECUTED ON : 09SEP2017` <br/>

### * Description
#### Name of module : OpenMRS Login page
This test determines the level of OpenMRS protection against leading space attack attempts on the login page.

### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally

### * Test Data
* Pair 1
Username: 5 empty spaces
Password: 5 empty spaces

* Pair 2
Username: admin
Password: 100 empty spaces followed by "password"

* Pair 3
Username: 100 empty spaces followed by "admin"
Password: 100 empty spaces followed by "password"

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.
2. Open up browser and go to "http://localhost:8081/openmrs-standalone/login.htm" (without the brackets)
3. Put in the value of pair 1 and click "login" button. Observe the OpenMRS 2.6.0 Standalone window (the one with the "Start" and "Stop" button)
4. Put in the value of pair 2 and click "login" button. Observe the OpenMRS 2.6.0 Standalone window (the one with the "Start" and "Stop" button)
5. Put in the value of pair 3 and click "login" button. Observe the OpenMRS 2.6.0 Standalone window (the one with the "Start" and "Stop" button)


### * Expected results
1. For pair 1, there must be a log with "INFO" type in the service console, saying "Failed login attempt - Empty username and password"
2. For pair 2, there must be a log with "INFO" type in the service console, saying "Failed login attempt - Username = admin and Password = password
3. For pair 3, there must be a log with "INFO" type in the service console, saying "Failed login attempt - Username = admin and Password = password

### * Post-condition
Login page is still available to whoever was doing the attack.

### * Actual results
1. There was no log in the service console after logging in with pair 1
2. With pair 2, post login log in the service console is "Failed login attempt (login=admin) - Invalid usrname and/or password : admin". This meeans the system was not able to record the mallicious string after large enough leading spaces.
3. There was no log in the service console after logging in with pair 3. This means with large enough trailing spaces, injection attacks on both username and password will go undetected

### * NOTES:
Contact tam.nguyen@ncsu.edu if you have problems following instructions in this test case.
# A7 - IAP - PROTECTION AGAINST AUTOMATIC SCAN
### Priority : medium
### Test status : FAILED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 09SEP2017` <br/>
`EXECUTED ON : 09SEP2017` <br/>

### * Description
#### Name of module : OpenMRS Login page
This test determines the level of OpenMRS protection against repeated, automatic attack attempts on the login page.

### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally

### * Test Data
Default rules that were pre-loaded in OWASP ZAP scanner

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.
2. Open up OWASP ZAP 2.6.0
3. From OWASP ZAP menu, go to Tools > Spider. In tab "Scope" box "Starting point", type : "http://localhost:8081/openmrs-standalone/login.htm" (without the brackets) and then click "Start Scan".
4. After the spider is done, from the OWASP ZAP main screen, type "http://localhost:8081/openmrs-standalone/login.htm" (without the brackets) into the box "URL to attack" and then click "Attack".
5. OWASP ZAP may relaunch the spider. At the bottom section, you may found the current tab is the "Spider" tab. After the spider is done, the program will automatically switch to the "Active " tab.
6. Monitor the column "Code" in OWASP ZAP scanner, the "Active Scan" tab and the OpenMRS 2.6.0 Standalone service console (the one with the "Tomcat port" and the "MySQL port" boxes)

### * Expected results
1. For each of OWASP ZAP's probe, the OpenMRS 2.6.0 Standalone console must give a description indicating a fail attempt at attacking the login page
2. After a certain number of attempts, server will throw a 4xx page (for example a "HTTP 400 - Bad Request" page)

### * Post-condition
Login page is made unavailable to whoever was doing the attack.

### * Actual results
1. There was no alert in the OpenMRS 2.6.0 Standalone console while more than 100 of probing attempts were carried out on the login page
2. Login page's status codes returned to OWASP ZAP were all "200"

### * NOTES:
Contact tam.nguyen@ncsu.edu if you have problems following instructions in this test case.
# A7 - CSRF - Change default language attack
### Priority : HIGH
### Test status : PASSED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 09SEP2017` <br/>
`EXECUTED ON : 09SEP2017` <br/>

### * Description
#### Name of module : OpenMRS default setting page

### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. A connection to the internet

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. Good connection to the internet

### * Test Data
http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?defaultLocale=fr

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start. The default language should be English. Login to OpenMRS
2. Go to "https://www.w3schools.com/tags/tryit.asp?filename=tryhtml_iframe"
3. At the W3School page, replace the value of iframe src with "http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?defaultLocale=fr" without the double quotes and click the "Run" button.
4. Go back to the homepage of OpenMRS and observe the language of the page

### * Expected results
In the iframe, OpenMRS server will give an error message

### * Post-condition
The OpenMRS service should still be able to run normally with the right language

### * Actual results
In the iframe, OpenMRS server gave an error message
"UI Framework Error - Root Error"

### * NOTES:
Contact tam.nguyen@ncsu.edu if you have problems following instructions in this test case.
# A7 - CSRF - COMMAND EXECUTION
### Priority : HIGH
### Test status : PASSED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 09SEP2017` <br/>
`EXECUTED ON : 09SEP2017` <br/>

### * Description
#### Name of module : OpenMRS help page
A different page will embed a link to OpenMRS. While the link appears to be normal (going to a known good site - the OpenMRS site), once the user clicks on it, it will launch an attack to the server under the logged in identity of the user. 

### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. A connection to the internet

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. Good connection to the internet

### * Test Data
http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=ZAP%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%0

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.
2. Go to "https://www.w3schools.com/tags/tryit.asp?filename=tryhtml_iframe"
3. At the W3School page, replace the value of iframe src with "http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=ZAP%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%0" without the double quotes and click the "Run" button.

4. Observe the result on the right iframe

### * Expected results
In the iframe, OpenMRS server will give an internal server error message
HTTP Status 500 - Request processing failed; nested exception is java.lang.IllegalArgumentException ...

### * Post-condition
The OpenMRS service should still be able to run normally

### * Actual results
In the iframe, OpenMRS server gave an internal server error message
HTTP Status 500 - Request processing failed; nested exception is java.lang.IllegalArgumentException ...

### * NOTES:
Contact tam.nguyen@ncsu.edu if you have problems following instructions in this test case.
# [A9 - UCKA] [ Finding Components with Known Vulnerabilities ]
`DESIGNER : [Xiangqing Ding]`
`UPDATED ON : [09/09/2017]`

### Name of module : [ Third Party Libraries & Database ]

### Priority : [low]

### Description
This case is listing all the components with known vulnerabilities. And describe some  related vulnerabilities.

### List of Components
1. Apache Tomcat:7.0.50
2. MySQL: Latest
3. JQuery: 1.12.4
4. Spring framework: 3.x
5. Hibernate: N/A
6. Java: Java 6 is minimal
6. JDK: JDK 7
7. Liquibase: 2.0


### Vulnerabilities
Module: Tomcat

Vulnerability: A malicious web application running on Apache Tomcat 9.0.0.M1 to 9.0.0.M9, 8.5.0 to 8.5.4, 8.0.0.RC1 to 8.0.36, 7.0.0 to 7.0.70 and 6.0.0 to 6.0.45 was able to bypass a configured SecurityManager via manipulation of the configuration parameters for the JSP Servlet

Link:[https://nvd.nist.gov/vuln/detail/CVE-2016-6796](https://nvd.nist.gov/vuln/detail/CVE-2016-6796)


Module: Hibernate

Vulnerability: ReflectionHelper (org.hibernate.validator.util.ReflectionHelper) in Hibernate Validator 4.1.0 before 4.2.1, 4.3.x before 4.3.2, and 5.x before 5.1.2 allows attackers to bypass Java Security Manager (JSM) restrictions and execute restricted reflection calls via a crafted application.

Link:[https://nvd.nist.gov/vuln/detail/CVE-2014-3558](https://nvd.nist.gov/vuln/detail/CVE-2014-3558)
# ZAP Scanning Report 1




## Summary of alerts

| Risk Level | Number of Alerts |
| --- | --- |
| High | 3 |
| Medium | 3 |
| Low | 4 |
| Informational | 0 |


## Alert details  

### SQL Injection
##### High (Medium)
  
  
  
  
#### Description
<p>SQL injection may be possible.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB?query=query+AND+1%3D1+--+](http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB?query=query+AND+1%3D1+--+)
  
  
  * Method: `GET`
  
  
  * Parameter: `query`
  
  
  * Attack: `query AND 1=1 -- `
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/login.page?query=query%27+AND+%271%27%3D%271](http://localhost:8081/openmrs-standalone/referenceapplication/login.page?query=query%27+AND+%271%27%3D%271)
  
  
  * Method: `GET`
  
  
  * Parameter: `query`
  
  
  * Attack: `query' AND '1'='1`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/login.htm?query=query+AND+1%3D1](http://localhost:8081/openmrs-standalone/login.htm?query=query+AND+1%3D1)
  
  
  * Method: `GET`
  
  
  * Parameter: `query`
  
  
  * Attack: `query AND 1=1`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB?query=query%27+AND+%271%27%3D%271%27+--+](http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB?query=query%27+AND+%271%27%3D%271%27+--+)
  
  
  * Method: `GET`
  
  
  * Parameter: `query`
  
  
  * Attack: `query' AND '1'='1' -- `
  
  
  
  
Instances: 4
  
### Solution
<p>Do not trust client side input, even if there is client side validation in place.  </p><p>In general, type check all data on the server side.</p><p>If the application uses JDBC, use PreparedStatement or CallableStatement, with parameters passed by '?'</p><p>If the application uses ASP, use ADO Command Objects with strong type checking and parameterized queries.</p><p>If database Stored Procedures can be used, use them.</p><p>Do *not* concatenate strings into queries in the stored procedure, or use 'exec', 'exec immediate', or equivalent functionality!</p><p>Do not create dynamic SQL queries using simple string concatenation.</p><p>Escape all data received from the client.</p><p>Apply a 'whitelist' of allowed characters, or a 'blacklist' of disallowed characters in user input.</p><p>Apply the principle of least privilege by using the least privileged database user possible.</p><p>In particular, avoid using the 'sa' or 'db-owner' database users. This does not eliminate SQL injection, but minimizes its impact.</p><p>Grant the minimum database access that is necessary for the application.</p>
  
### Other information
<p>The page results were successfully manipulated using the boolean conditions [query AND 1=1 -- ] and [query AND 1=2 -- ]</p><p>The parameter value being modified was NOT stripped from the HTML output for the purposes of the comparison</p><p>Data was returned for the original parameter.</p><p>The vulnerability was detected by successfully restricting the data originally returned, by manipulating the parameter</p>
  
### Reference
* https://www.owasp.org/index.php/Top_10_2010-A1
* https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet

  
#### CWE Id : 89
  
#### WASC Id : 19
  
#### Source ID : 1

  
  
  
### Cross Site Scripting (Reflected)
##### High (Medium)
  
  
  
  
#### Description
<p>Cross-site Scripting (XSS) is an attack technique that involves echoing attacker-supplied code into a user's browser instance. A browser instance can be a standard web browser client, or a browser object embedded in a software product such as the browser within WinAmp, an RSS reader, or an email client. The code itself is usually written in HTML/JavaScript, but may also extend to VBScript, ActiveX, Java, Flash, or any other browser-supported technology.</p><p>When an attacker gets a user's browser to execute his/her code, the code will run within the security context (or zone) of the hosting web site. With this level of privilege, the code has the ability to read, modify and transmit any sensitive data accessible by the browser. A Cross-site Scripted user could have his/her account hijacked (cookie theft), their browser redirected to another location, or possibly shown fraudulent content delivered by the web site they are visiting. Cross-site Scripting attacks essentially compromise the trust relationship between a user and the web site. Applications utilizing browser object instances which load content from the file system may execute code under the local machine zone allowing for system compromise.</p><p></p><p>There are three types of Cross-site Scripting attacks: non-persistent, persistent and DOM-based.</p><p>Non-persistent attacks and DOM-based attacks require a user to either visit a specially crafted link laced with malicious code, or visit a malicious web page containing a web form, which when posted to the vulnerable site, will mount the attack. Using a malicious form will oftentimes take place when the vulnerable resource only accepts HTTP POST requests. In such a case, the form can be submitted automatically, without the victim's knowledge (e.g. by using JavaScript). Upon clicking on the malicious link or submitting the malicious form, the XSS payload will get echoed back and will get interpreted by the user's browser and execute. Another technique to send almost arbitrary requests (GET and POST) is by using an embedded client, such as Adobe Flash.</p><p>Persistent attacks occur when the malicious code is submitted to a web site where it's stored for a period of time. Examples of an attacker's favorite targets often include message board posts, web mail messages, and web chat software. The unsuspecting user is not required to interact with any additional site/link (e.g. an attacker site or a malicious link sent via email), just simply view the web page containing the code.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=%27%3Balert%281%29%3B%27](http://localhost:8081/openmrs-standalone/help.htm?lang=%27%3Balert%281%29%3B%27)
  
  
  * Method: `GET`
  
  
  * Parameter: `lang`
  
  
  * Attack: `';alert(1);'`
  
  
  * Evidence: `';alert(1);'`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/login.htm](http://localhost:8081/openmrs-standalone/login.htm)
  
  
  * Method: `POST`
  
  
  * Parameter: `sessionLocation`
  
  
  * Attack: `</pre><script>alert(1);</script><pre>`
  
  
  * Evidence: `</pre><script>alert(1);</script><pre>`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB](http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB)
  
  
  * Method: `POST`
  
  
  * Parameter: `sessionLocation`
  
  
  * Attack: `</pre><script>alert(1);</script><pre>`
  
  
  * Evidence: `</pre><script>alert(1);</script><pre>`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=%27%3Balert%281%29%3B%27](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=%27%3Balert%281%29%3B%27)
  
  
  * Method: `GET`
  
  
  * Parameter: `lang`
  
  
  * Attack: `';alert(1);'`
  
  
  * Evidence: `';alert(1);'`
  
  
  
  
Instances: 4
  
### Solution
<p>Phase: Architecture and Design</p><p>Use a vetted library or framework that does not allow this weakness to occur or provides constructs that make this weakness easier to avoid.</p><p>Examples of libraries and frameworks that make it easier to generate properly encoded output include Microsoft's Anti-XSS library, the OWASP ESAPI Encoding module, and Apache Wicket.</p><p></p><p>Phases: Implementation; Architecture and Design</p><p>Understand the context in which your data will be used and the encoding that will be expected. This is especially important when transmitting data between different components, or when generating outputs that can contain multiple encodings at the same time, such as web pages or multi-part mail messages. Study all expected communication protocols and data representations to determine the required encoding strategies.</p><p>For any data that will be output to another web page, especially any data that was received from external inputs, use the appropriate encoding on all non-alphanumeric characters.</p><p>Consult the XSS Prevention Cheat Sheet for more details on the types of encoding and escaping that are needed.</p><p></p><p>Phase: Architecture and Design</p><p>For any security checks that are performed on the client side, ensure that these checks are duplicated on the server side, in order to avoid CWE-602. Attackers can bypass the client-side checks by modifying values after the checks have been performed, or by changing the client to remove the client-side checks entirely. Then, these modified values would be submitted to the server.</p><p></p><p>If available, use structured mechanisms that automatically enforce the separation between data and code. These mechanisms may be able to provide the relevant quoting, encoding, and validation automatically, instead of relying on the developer to provide this capability at every point where output is generated.</p><p></p><p>Phase: Implementation</p><p>For every web page that is generated, use and specify a character encoding such as ISO-8859-1 or UTF-8. When an encoding is not specified, the web browser may choose a different encoding by guessing which encoding is actually being used by the web page. This can cause the web browser to treat certain sequences as special, opening up the client to subtle XSS attacks. See CWE-116 for more mitigations related to encoding/escaping.</p><p></p><p>To help mitigate XSS attacks against the user's session cookie, set the session cookie to be HttpOnly. In browsers that support the HttpOnly feature (such as more recent versions of Internet Explorer and Firefox), this attribute can prevent the user's session cookie from being accessible to malicious client-side scripts that use document.cookie. This is not a complete solution, since HttpOnly is not supported by all browsers. More importantly, XMLHTTPRequest and other powerful browser technologies provide read access to HTTP headers, including the Set-Cookie header in which the HttpOnly flag is set.</p><p></p><p>Assume all input is malicious. Use an "accept known good" input validation strategy, i.e., use a whitelist of acceptable inputs that strictly conform to specifications. Reject any input that does not strictly conform to specifications, or transform it into something that does. Do not rely exclusively on looking for malicious or malformed inputs (i.e., do not rely on a blacklist). However, blacklists can be useful for detecting potential attacks or determining which inputs are so malformed that they should be rejected outright.</p><p></p><p>When performing input validation, consider all potentially relevant properties, including length, type of input, the full range of acceptable values, missing or extra inputs, syntax, consistency across related fields, and conformance to business rules. As an example of business rule logic, "boat" may be syntactically valid because it only contains alphanumeric characters, but it is not valid if you are expecting colors such as "red" or "blue."</p><p></p><p>Ensure that you perform input validation at well-defined interfaces within the application. This will help protect the application even if a component is reused or moved elsewhere.</p>
  
### Reference
* http://projects.webappsec.org/Cross-Site-Scripting
* http://cwe.mitre.org/data/definitions/79.html

  
#### CWE Id : 79
  
#### WASC Id : 8
  
#### Source ID : 1

  
  
  
### SQL Injection - Authentication Bypass
##### High (Medium)
  
  
  
  
#### Description
<p>SQL injection may be possible on a login page, potentially allowing the application's authentication mechanism to be bypassed </p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/login.htm](http://localhost:8081/openmrs-standalone/login.htm)
  
  
  * Method: `GET`
  
  
  * Parameter: `query`
  
  
  * Attack: `query AND 1=1`
  
  
  
  
Instances: 1
  
### Solution
<p>Do not trust client side input, even if there is client side validation in place.  </p><p>In general, type check all data on the server side.</p><p>If the application uses JDBC, use PreparedStatement or CallableStatement, with parameters passed by '?'</p><p>If the application uses ASP, use ADO Command Objects with strong type checking and parameterized queries.</p><p>If database Stored Procedures can be used, use them.</p><p>Do *not* concatenate strings into queries in the stored procedure, or use 'exec', 'exec immediate', or equivalent functionality!</p><p>Do not create dynamic SQL queries using simple string concatenation.</p><p>Escape all data received from the client.</p><p>Apply a 'whitelist' of allowed characters, or a 'blacklist' of disallowed characters in user input.</p><p>Apply the principle of least privilege by using the least privileged database user possible.</p><p>In particular, avoid using the 'sa' or 'db-owner' database users. This does not eliminate SQL injection, but minimizes its impact.</p><p>Grant the minimum database access that is necessary for the application.</p>
  
### Reference
* https://www.owasp.org/index.php/Top_10_2010-A1
* https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet

  
#### CWE Id : 89
  
#### WASC Id : 19
  
#### Source ID : 1

  
  
  
### X-Frame-Options Header Not Set
##### Medium (Medium)
  
  
  
  
#### Description
<p>X-Frame-Options header is not included in the HTTP response to protect against 'ClickJacking' attacks.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=fr](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=fr)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=fr](http://localhost:8081/openmrs-standalone/help.htm?lang=fr)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm](http://localhost:8081/openmrs-standalone/help.htm)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=en_US](http://localhost:8081/openmrs-standalone/help.htm?lang=en_US)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=pt](http://localhost:8081/openmrs-standalone/help.htm?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=pt&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=pt&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/](http://localhost:8081/openmrs-standalone/)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=es&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=es&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=it](http://localhost:8081/openmrs-standalone/help.htm?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB](http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=es](http://localhost:8081/openmrs-standalone/help.htm?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_US&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_US&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_GB&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_GB&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/login.htm](http://localhost:8081/openmrs-standalone/login.htm)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=pt](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
Instances: 25
  
### Solution
<p>Most modern Web browsers support the X-Frame-Options HTTP header. Ensure it's set on all web pages returned by your site (if you expect the page to be framed only by pages on your server (e.g. it's part of a FRAMESET) then you'll want to use SAMEORIGIN, otherwise if you never expect the page to be framed, you should use DENY. ALLOW-FROM allows specific websites to frame the web page in supported web browsers).</p>
  
### Reference
* http://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx

  
#### CWE Id : 16
  
#### WASC Id : 15
  
#### Source ID : 3

  
  
  
### Application Error Disclosure
##### Medium (Medium)
  
  
  
  
#### Description
<p>This page contains an error/warning message that may disclose sensitive information like the location of the file that produced the unhandled exception. This information can be used to launch further attacks against the web application. The alert could be a false positive if the error message is found inside a documentation page.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles/styleguide](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles/styleguide)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms](http://localhost:8081/openmrs-standalone/ms)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/styles)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/images](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/images)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/images](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/images)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/images/logo](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/images/logo)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
Instances: 10
  
### Solution
<p>Review the source code of this page. Implement custom error pages. Consider implementing a mechanism to provide a unique error reference/identifier to the client (browser) while logging the details on the server side and not exposing them to the user.</p>
  
### Reference
* 

  
#### CWE Id : 200
  
#### WASC Id : 13
  
#### Source ID : 3

  
  
  
### Format String Error
##### Medium (Medium)
  
  
  
  
#### Description
<p>A Format String error occurs when the submitted data of an input string is evaluated as a command by the application. </p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=ZAP%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%0A](http://localhost:8081/openmrs-standalone/help.htm?lang=ZAP%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%0A)
  
  
  * Method: `GET`
  
  
  * Parameter: `lang`
  
  
  * Attack: `ZAP%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s
`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=ZAP%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%0A](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=ZAP%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%0A)
  
  
  * Method: `GET`
  
  
  * Parameter: `lang`
  
  
  * Attack: `ZAP%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s
`
  
  
  
  
Instances: 2
  
### Solution
<p>Rewrite the background program using proper deletion of bad character strings.  This will require a recompile of the background executable.</p>
  
### Other information
<p>Potential Format String Error.  The script closed the connection on a /%s</p>
  
### Reference
* https://www.owasp.org/index.php/Format_string_attack

  
#### CWE Id : 134
  
#### WASC Id : 6
  
#### Source ID : 1

  
  
  
### Cookie No HttpOnly Flag
##### Low (Medium)
  
  
  
  
#### Description
<p>A cookie has been set without the HttpOnly flag, which means that the cookie can be accessed by JavaScript. If a malicious script can be run on this page then the cookie will be accessible and can be transmitted to another site. If this is a session cookie then session hijacking may be possible.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=en_US](http://localhost:8081/openmrs-standalone/help.htm?lang=en_US)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=pt](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=fr](http://localhost:8081/openmrs-standalone/help.htm?lang=fr)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=pt](http://localhost:8081/openmrs-standalone/help.htm?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=es](http://localhost:8081/openmrs-standalone/help.htm?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_GB](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_GB)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=it](http://localhost:8081/openmrs-standalone/help.htm?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=en_GB](http://localhost:8081/openmrs-standalone/help.htm?lang=en_GB)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=fr](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=fr)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
Instances: 12
  
### Solution
<p>Ensure that the HttpOnly flag is set for all cookies.</p>
  
### Reference
* http://www.owasp.org/index.php/HttpOnly

  
#### CWE Id : 16
  
#### WASC Id : 13
  
#### Source ID : 3

  
  
  
### Web Browser XSS Protection Not Enabled
##### Low (Medium)
  
  
  
  
#### Description
<p>Web Browser XSS Protection is not enabled, or is disabled by the configuration of the 'X-XSS-Protection' HTTP response header on the web server</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/styles)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/%7B%7B=%20breadcrumb.link%20%7D%7D](http://localhost:8081/openmrs-standalone/%7B%7B=%20breadcrumb.link%20%7D%7D)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=es](http://localhost:8081/openmrs-standalone/help.htm?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_GB&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_GB&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/myAccount.page](http://localhost:8081/openmrs-standalone/adminui/myaccount/myAccount.page)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication](http://localhost:8081/openmrs-standalone/referenceapplication)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_GB](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_GB)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=it](http://localhost:8081/openmrs-standalone/help.htm?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_US&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_US&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/](http://localhost:8081/openmrs-standalone/)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/%7B%7B=%20breadcrumb.link%20%7D%7D](http://localhost:8081/openmrs-standalone/adminui/myaccount/%7B%7B=%20breadcrumb.link%20%7D%7D)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm](http://localhost:8081/openmrs-standalone/help.htm)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=pt](http://localhost:8081/openmrs-standalone/help.htm?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
Instances: 39
  
### Solution
<p>Ensure that the web browser's XSS filter is enabled, by setting the X-XSS-Protection HTTP response header to '1'.</p>
  
### Other information
<p>The X-XSS-Protection HTTP response header allows the web server to enable or disable the web browser's XSS protection mechanism. The following values would attempt to enable it: </p><p>X-XSS-Protection: 1; mode=block</p><p>X-XSS-Protection: 1; report=http://www.example.com/xss</p><p>The following values would disable it:</p><p>X-XSS-Protection: 0</p><p>The X-XSS-Protection HTTP response header is currently supported on Internet Explorer, Chrome and Safari (WebKit).</p><p>Note that this alert is only raised if the response body could potentially contain an XSS payload (with a text-based content type, with a non-zero length).</p>
  
### Reference
* https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet
* https://blog.veracode.com/2014/03/guidelines-for-setting-security-headers/

  
#### CWE Id : 933
  
#### WASC Id : 14
  
#### Source ID : 3

  
  
  
### X-Content-Type-Options Header Missing
##### Low (Medium)
  
  
  
  
#### Description
<p>The Anti-MIME-Sniffing header X-Content-Type-Options was not set to 'nosniff'. This allows older versions of Internet Explorer and Chrome to perform MIME-sniffing on the response body, potentially causing the response body to be interpreted and displayed as a content type other than the declared content type. Current (early 2014) and legacy versions of Firefox will use the declared content type (if one is set), rather than performing MIME-sniffing.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/jquery.toastmessage.js?cache=1504310202510](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/jquery.toastmessage.js?cache=1504310202510)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/underscore-min.js?cache=1504310202510](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/underscore-min.js?cache=1504310202510)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/fontawesome-webfont.woff?v=3.0.1](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/fontawesome-webfont.woff?v=3.0.1)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/opensans-regular-webfont.ttf](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/opensans-regular-webfont.ttf)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/moduleResources/legacyui/css/style.css?v=2.0.5](http://localhost:8081/openmrs-standalone/moduleResources/legacyui/css/style.css?v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=it&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=it&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/emr.js?cache=1504310202510](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/emr.js?cache=1504310202510)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=pt](http://localhost:8081/openmrs-standalone/help.htm?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/home.page](http://localhost:8081/openmrs-standalone/referenceapplication/home.page)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/icomoon.woff](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/icomoon.woff)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles/header.css?cache=1504310202510](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles/header.css?cache=1504310202510)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=es](http://localhost:8081/openmrs-standalone/help.htm?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/moduleResources/legacyui/css/openmrs.css?v=2.0.5](http://localhost:8081/openmrs-standalone/moduleResources/legacyui/css/openmrs.css?v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/jquery-1.12.4.min.js?cache=1504310202510](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/jquery-1.12.4.min.js?cache=1504310202510)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=es&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=es&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/login.htm](http://localhost:8081/openmrs-standalone/login.htm)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=it](http://localhost:8081/openmrs-standalone/help.htm?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
Instances: 53
  
### Solution
<p>Ensure that the application/web server sets the Content-Type header appropriately, and that it sets the X-Content-Type-Options header to 'nosniff' for all web pages.</p><p>If possible, ensure that the end user uses a standards-compliant and modern web browser that does not perform MIME-sniffing at all, or that can be directed by the web application/web server to not perform MIME-sniffing.</p>
  
### Other information
<p>This issue still applies to error type pages (401, 403, 500, etc) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.</p><p>At "High" threshold this scanner will not alert on client or server error responses.</p>
  
### Reference
* http://msdn.microsoft.com/en-us/library/ie/gg622941%28v=vs.85%29.aspx
* https://www.owasp.org/index.php/List_of_useful_HTTP_headers

  
#### CWE Id : 16
  
#### WASC Id : 15
  
#### Source ID : 3

  
  
  
### Content-Type Header Missing
##### Low (Medium)
  
  
  
  
#### Description
<p>The Content-Type header was either missing or empty.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/opensans-regular-webfont.ttf](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/opensans-regular-webfont.ttf)
  
  
  * Method: `GET`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/icomoon.woff](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/icomoon.woff)
  
  
  * Method: `GET`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/fontawesome-webfont.woff?v=3.0.1](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/fontawesome-webfont.woff?v=3.0.1)
  
  
  * Method: `GET`
  
  
  
  
Instances: 3
  
### Solution
<p>Ensure each page is setting the specific and appropriate content-type value for the content being delivered.</p>
  
### Reference
* http://msdn.microsoft.com/en-us/library/ie/gg622941%28v=vs.85%29.aspx

  
#### CWE Id : 345
  
#### WASC Id : 12
  
#### Source ID : 3
This open-source systems provides electronic health care functionality for “resource-constrained environments”.   While the system has not been designed for deployment within the United States, security and privacy concerns are still a paramount security concern for any patient.

For the first phase of the project, we will perform a security review based upon the OWASP Top 10 (use the 2017 RC1 version).  Our team will be responsible for documenting the findings and providing remediation suggestions to correct and adverse findings. 

## Software:
OpenMRS 2.6:  The standalone version is sufficient: (http://openmrs.org/download/)
For A10, we will use the OpenMRS REST Module: https://wiki.openmrs.org/display/docs/REST+Module

## Deliverables:<br/>
### 1. OWASP Top Ten (Ethical Hack Test Plan and Execution)<br/>
Repeatable black box test plan for the OWASP Top 10 Vulnerabilities.  For each of the Top 10 vulnerability, we create two repeatable test cases.  For each test case, we provide:
* A unique test case id
* Repeatable instructions for how to execute the test case
* Expected results when running the test case
For A9 (“Using Components with Known Vulnerabilities”), we will list the third-party software libraries the application uses as well as the database management system (DBMS) software.  Additionally, we will search at least 2 of the libraries and the DBMS name/version to see if any known vulnerabilities exist and document whether such vulnerabilities exist.  If vulnerabilities do exist, we will provide a brief sentence describing at least one with a link to the originating source material.

### 2. Run the test cases on OpenMRS (Version 2.6).<br/>
For each test case, we will report the actual results of running compared with the expected results and whether the test cases passes (indicating the system is secure) or fails (indicating the system is insecure).  We will describe the vulnerability and what it would take to stress the system to see if the vulnerability exists.  

### 3. For each of the Top 10, we will summarize our test results<br/>
If we do not find any vulnerabilities, document how we tested for each vulnerability and how the OpenMRS development team mitigated against such attacks.  
If we find a vulnerability, document repeatable instructions for replicating the vulnerability that should be submitted to OpenMRS.
# [Test ID ] [ TEST CASE TITLE ]
### Priority : [low - medium - high]
### Test status : [ fail - pass ]
`DESIGNER : [test designer name - all caps]` <br/>
`EXECUTED BY : [executer name - all caps]` <br/>
`UPDATED ON : [creation or update date]` <br/>
`EXECUTED ON : [execution date of test]` <br/>

### * Description
#### Name of module : [details of module tested here - ie a web page]
Determine the summary or test purpose in brief

### * Precondition
Any requirement that needs to be done before execution of this test case. To execute this test case list all pre-conditions (ie. JRE installed, SQL installed...)

### * Dependencies
Determine any dependencies on test requirements or other test cases

### * Test Data
Use of test data as an input for the test case. Deliver different data sets with precise values to be used as an input. Note that this can be all possible data (ie. all possible pairs of default usernames, default passwords)

### * Test steps
1. List specifics step 1
2. List specifics step 2
3. Step 3
4. Please be as specific as possible

### * Expected results
Mention the expected result including error or message that should appear on screen
### * Post-condition
What would be the state of the system after running the test case?
### * Actual results
After test execution, actual test result should be filled
### * NOTES:
Put your extra notes here
Might as well put links to related resources (like you seen in the scan reports)