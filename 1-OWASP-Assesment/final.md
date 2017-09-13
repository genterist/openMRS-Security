# A1 - Injection - Drop Table
`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [09/09/2017]`

### Name of module : Search module

### Priority : [high]

### Test Description
Injection attacks occur when unvalidated input is embedded in an instruction stream and cannot be distinguished from valid instructions.
This test will test if an attacker can use SQL injection to drop a table

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
test'; DROP TABLE Patients; #

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Input " test'; DROP TABLE Patients; #" (without the double quotes) in the search field

<<we need to put additional step to verify if table patients was drop or not in here>>

### * Expected results
1. No result will be shown

### * Actual results
 No result showed

### Test status : [ PASS ]


# A1 - Injection - Tautology
`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [09/09/2017]`

### Name of module : Login Module

### Priority : [high]

### Test Description
Injection attacks occur when unvalidated input is embedded in an instruction stream and cannot be distinguished from valid instructions.
This test will test if an attack can use SQL injection to bypass login.

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
2. Log in with the username and password mentioned in Test Data section

### * Expected results
1. Fail to login

### * Actual results
Login Failed

### Test status : [ pass ]


# A2 - BAC -Exposed Session IDs
`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [09/09/2017]`

### Name of module : entire site

### Priority : [high]

### Test Description : Broken Access Control 
Access control, sometimes called authorization, is how a web application grants access to content and functions to some users and not others. These checks are performed after authentication, and govern what 'authorized' users are allowed to do. This test will check if session ID or important access control data will be exposed on URLs or not.

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
1. Start local openMRS and log in with the username and password mentioned in Test Data section
2. Browsing the system and observe the urls

### * Expected results
1. No session related infomation will be exposed in the urls

### * Actual results
No session infomation exposed

### Test status : [ pass ]


# [A2 - BAC] [ Session Time Outs ]
`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [09/09/2017]`

### Name of module : Login module

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

### Test status : [ fail ]#



A4 - BAC - Unauthorized access to system
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
* Contact tam.nguyen@ncsu.edu if you have problems following instructions in this test case.