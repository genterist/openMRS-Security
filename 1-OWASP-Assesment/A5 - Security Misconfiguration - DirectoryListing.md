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

