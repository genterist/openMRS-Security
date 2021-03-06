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
