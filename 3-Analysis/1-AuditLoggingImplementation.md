# Audit/Logging Ismplementation #

## Test case: U-1

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Update ]

### Test Description
When someone adds a patient’s information, the username, IP address, and time should be logged.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2.	Click “Register a patient” in the main page
3.	Input Kobe in Given field and Bryant in Family Name field
4.	Choose Male as gender
5.	Let the birthday be 8/23/1978
6.	Address as Staples Center, Los Angeles, CA, Los Angeles, 90001
7.	Phone 555-555-5555
8.	No relatives

### * Expected logged info
1. username
2. time
3. ip address
4. computer id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 14:17:28,252| In method PatientService.savePatient. Arguments: Patient=Patient#null, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 14:17:28,279| Exiting method savePatient
INFO - LoggingAdvice.invoke(115) |2017-10-24 14:17:28,738| In method UserService.saveUser. Arguments: User=admin, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 14:17:28,745| Exiting method saveUser

### Test status : [ fail ]

No IP address or computer ID is tracked. 
It is inadequate because you cannot tell whether it was operated by the person.



# Test case: U-2

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Update ]

### Test Description
When someone registers a new patient, his password and session id should not be logged.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2.	Click “Register a patient” in the main page
3.	Input Kobe in Given field and Bryant in Family Name field
4.	Choose Male as gender
5.	Let the birthday be 8/23/1978
6.	Address as Staples Center, Los Angeles, CA, Los Angeles, 90001
7.	Phone 555-555-5555
8.	No relatives

### * Expected logged info
1. Not include user password or session id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 14:17:28,252| In method PatientService.savePatient. Arguments: Patient=Patient#null, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 14:17:28,279| Exiting method savePatient
INFO - LoggingAdvice.invoke(115) |2017-10-24 14:17:28,738| In method UserService.saveUser. Arguments: User=admin, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 14:17:28,745| Exiting method saveUser

### Test status : [ fail ]

The password and session id is not be logged 




# Test case: U-3

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Update ]

### Test Description
When someone update a patient’s information, the username, IP address, and time should be logged.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”
4. Click “Edit”
5. Change the first name to “Koby”
6. Confirm

### * Expected logged info
1. username
2. time
3. ip address
4. computer id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:01:45,960| In method PatientService.savePatient. Arguments: Patient=Patient#108, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:01:45,996| Exiting method savePatient
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:01:46,297| In method UserService.saveUser. Arguments: User=admin, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:01:46,301| Exiting method saveUser

### Test status : [ fail ]

No IP address or computer ID is tracking. 
It is inadequate because you cannot tell whether it was operated by the person.




# Test case: U-4

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Update ]

### Test Description
When someone updates a new patient, his password and session id should not be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”
4. Click “Edit”
5. Change the first name to “Koby”
6. Confirm

### * Expected logged info
user password or session id should not be logged

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:01:45,960| In method PatientService.savePatient. Arguments: Patient=Patient#108, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:01:45,996| Exiting method savePatient
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:01:46,297| In method UserService.saveUser. Arguments: User=admin, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:01:46,301| Exiting method saveUser

### Test status : [ pass ]

No private information is exposed




# Test case: U-5

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Update ]

### Test Description
When someone deletes a patient’s information, the username, IP address, and time should be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”
4. Click “Delete Patient”
5. Input “He has no problem” as the reason.
6. Input username and password
7. Confrim

### * Expected logged info
1. username
2. time
3. ip address
4. computer id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:46:59,026| In method PatientService.voidPatient. Arguments: Patient=Patient#108, String=He has no problem, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:46:59,086| Exiting method voidPatient

### Test status : [ fail ]

No IP address or computer ID is tracking. 
It is inadequate because you cannot tell whether it was operated by the person.




# Test case: D-1

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ Delete ]

### Test Description
When someone deletes a new patient, his password and session id should not be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”
4. Click “Delete Patient”
5. Input “He has no problem” as the reason.
6. Input username and password
7. Confrim

### * Expected logged info
user password or session id should not be logged

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 16:46:59,026| In method PatientService.voidPatient. Arguments: Patient=Patient#108, String=He has no problem, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 16:46:59,086| Exiting method voidPatient

### Test status : [ pass ]

No private information is exposed



# Test case: V-1

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ View ]

### Test Description
When someone views a patient’s information, the username, IP address, and time should be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”


### * Expected logged info
1. username
2. time
3. ip address
4. computer id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 17:01:36,095| In method UserService.saveUser. Arguments: User=nurse, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 17:01:36,098| Exiting method saveUser

### Test status : [ fail ]

No IP address or computer ID is tracking. 
It is inadequate because you cannot tell whether it was operated by the person.



# Test case: V-2

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ View ]

### Test Description
When someone views a new patient, his password and session id should not be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Find Patient Record” in the main page
3. Click “Kobe Bryant”

### * Expected logged info
user password or session id should not be logged

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 17:01:36,095| In method UserService.saveUser. Arguments: User=nurse, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 17:01:36,098| Exiting method saveUser

### Test status : [ pass ]

No private information is exposed.


# Test case: V-3

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ View ]

### Test Description
When someone views a patient’s information, the username, IP address, and time should be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Admin`
2. Password: `Admin123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Appointment Scheduling” in the main page
3. Click “Manage Appointment”
4. Input “Kobe Bryant” and search


### * Expected logged info
1. username
2. time
3. ip address
4. computer id

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 17:01:36,095| In method UserService.saveUser. Arguments: User=nurse, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 17:01:36,098| Exiting method saveUser

### Test status : [ fail ]


No IP address or computer ID is tracking. 
It is inadequate because you cannot tell whether it was operated by the person.



# Test case: V-4

`DESIGNER : [Fuxing Luan]`
`UPDATED ON : [10/24/2017]`

### Name of module : [ View ]

### Test Description
When someone views a new patient's appointment, his password and session id should not be logged

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped
4. Latest Chrome browser

### * Assumption
3. OpenMRS with demo database runs normally

### * Test Data
1. Username: `Nurse`
2. Password: `Nurse123`

### * Test steps
1. Start local openMRS and log in with the username and account
2. Click “Appointment Scheduling” in the main page
3. Click “Manage Appointment”
4. Input “Kobe Bryant” and search

### * Expected logged info
user password or session id should not be logged

### * Actual results
INFO - LoggingAdvice.invoke(115) |2017-10-24 17:01:36,095| In method UserService.saveUser. Arguments: User=nurse, 
INFO - LoggingAdvice.invoke(155) |2017-10-24 17:01:36,098| Exiting method saveUser

### Test status : [ pass ]

No private information is exposed.

