# [ A4 - BAC ] [ Unauthorized access to system ]
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

### * Test steps
1. Start local openMRS
![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A4-02-01.PNG)
2. Without logging in, put `http://localhost:8081/openmrs-standalone/referenceapplication/home.page` in the URL of browser.
![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A4-02-02.PNG)
3. Direct the URL to see if it can access to the system.

### * Expected results
User cannot access to the main page without logging in

### * Actual results
No response from the page. User cannot access to the main page without logging in

### Test status : [ pass ]