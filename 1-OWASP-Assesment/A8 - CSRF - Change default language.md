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
