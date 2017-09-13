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

![User is not logged in [Privileges required: Get Users](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Result/A10-API-Authentication.PNG?raw=true)


### * NOTES:
* OpenMRS API documentation together with examples can be found at http://localhost:8081/openmrs-standalone/module/webservices/rest/apiDocs.htm (logged in as admin first)
You can expand the objects and click "try it out" to get sample codes.
* You can install the OpenMRS webservice API by downloading it from https://modules.openmrs.org/#/show/153/webservices-rest and then move the downloaded file to [download folder]\referenceapplication-standalone-2.6.0\appdata\modules
* Contact tam.nguyen@ncsu.edu if you have problems following instructions in this test case.