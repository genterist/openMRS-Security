# [A5 - Security Misconfiguration ] [ Default username and password]
### Test status : [ pass ]
`DESIGNER : [ZHUO LI]` <br/>
`UPDATED ON : [05SEP2017]` <br/>

### * Description

This test verifies there is no default username and password which can be used by hackers.

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
1. Go to http://localhost:8081/openmrs-standalone/login.htm
2. Try to login with default user name and password  (listed in Test Data section)

### * Expected results
There should be no default user name and password and tester should not be able to logon

### * Actual results
Log in failed with test username and password.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Result/A5_001.PNG)
