# [A1 - Injection] [ Tautology ]
`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [09/09/2017]`

### Name of module : [ Login ]

### Priority : [high]

### Test Description
Injection attacks occur when unvalidated input is embedded in an instruction stream and cannot be distinguished from valid instructions. This test case is to test whether using tautology can bypass password authentication.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
1. Username: ’ OR ‘1’ = ‘1 
2. Password: ’ OR ‘1’ = ‘1 

![alt text](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Result/A1_003.png?raw=true)

### * Test steps
1. Start local openMRS and 
2. Log in with the username and account

### * Expected results
1. Fail to login

### * Actual results
Login Failed

### Test status : [ pass ]
