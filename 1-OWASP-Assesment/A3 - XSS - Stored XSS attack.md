# [ A3 - XSS ] [ Detecting Stored XSS ]
`DESIGNER : [Xiangqing Ding]`
`UPDATED ON : [09/09/2017]`

### Name of module : [ Allergy page ]

### Priority : [high]

### Test Description


XSS attacks are essentially code injection attacks into the various interpreters in the browser. This test case is trying to see if script can be stored and executed in the allergy page.

### * Precondition
1. A local computer with administrator privilege
2. Java environment installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unzipped

### * Assumption
1. OpenMRS with demo database runs normally

### * Test Data
1. Username: `nurse`
2. Password: `Nurse123`
3. Script: `<script>alert("Attacked")</script>`

### * Test steps
1. Start openMRS and log in with username and password provided
2. Click “Find Patient Record” button in the main page
3. Search one of the patient (e.g. Christopher Allen) and go to the patient page by clicking the entry
4. In the patient page, find ALLERGIES column and click the edit button
5. In the allergy page, click “Add New Allergy” button to add a new allergy
6. In the “comment” field, add the script. Other field can be filled with own choice. After that, save the allergy.
7. Go to the allergy page again to see if there is a popup with message “Attacked”

### * Expected results
1. The script is not accepted
2. The script is accepted but changed to valid form
3. The script is accepted but not executed

### * Actual results
The script is accepted but doesn’t work

### Test status : [ pass ]