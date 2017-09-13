# [A2 - BAC] [ Session Time Outs ]
`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [09/09/2017]`

### Name of module : [ Session ]

### Priority : [high]

### Test Description : Broken Access Control 
Access control, sometimes called authorization, is how a web application grants access to content and functions to some users and not others. These checks are performed after authentication, and govern what 'authorized' users are allowed to do. In this test, we will test whether the session is ended when the browser closes.

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
