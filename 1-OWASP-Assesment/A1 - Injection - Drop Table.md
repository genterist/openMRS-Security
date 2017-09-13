# [A1 - Injection] [ Drop Table ]
`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [09/09/2017]`

### Name of module : [ Search ]

### Priority : [high]

### Test Description
Injection attacks occur when unvalidated input is embedded in an instruction stream and cannot be distinguished from valid instructions. This test is to see whether using SQL key words in the search fields will affect the database.

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
2. Click “Find Patient Record” in the main page
3. Input a'; Drop Table Patients;" in the search field

### * Expected results
1. No result will be shown
2. Existed patients will not be deleted

### * Actual results
 No result showed
 Exisited patients still there

### Test status : [ pass ]
