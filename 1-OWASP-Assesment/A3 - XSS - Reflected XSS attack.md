# [A3 - XSS] [ Detecting Reflected XSS ]
`DESIGNER : [Xiangqing Ding]`
`UPDATED ON : [09/12/2017]`

### Name of module : [ Search field in Find Patient Record ]

### Priority : [high]

### Test Description
XSS attacks are essentially code injection attacks into the various interpreters in the browser. This test case is trying to detect if a script can be integrated in HTML and executed.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test steps
1. Start local openMRS and log in with the username (`nurse`) and password (`Nurse123`)

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-01-01.PNG)


2. Click “Find Patient Record” in the main page

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-01-02.PNG)


3. Input script (`<script>alert("Attacked")</script>`) in the search field and search

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-01-03.PNG)


4. Input script (`%3cscript%3e alert("Attacked") %3cscript%3e`) in the search field and search

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-01-04.PNG)


### * Expected results
1. Scripts are not accepted
2. Scripts are accepted but not executed

### * Actual results
Scripts are accepted but not executed.

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-01-03.PNG)

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-01-04.PNG)

### Test status : [ Pass ]