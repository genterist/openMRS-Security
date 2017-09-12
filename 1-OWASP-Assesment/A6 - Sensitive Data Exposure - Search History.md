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