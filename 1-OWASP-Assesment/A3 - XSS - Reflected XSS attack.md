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

### Test status : [ pass ]