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

### * Test steps
1. Start openMRS and log in with username(`nurse`) and password(`Nurse123`)

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-02-01.PNG)

2. Click “Find Patient Record” button in the main page

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-02-02.PNG)


3. Search one of the patient (e.g. Christopher Allen) and go to the patient page by clicking the entry

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-02-03.PNG)


4. In the patient page, find ALLERGIES column and click the edit button

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-02-04.PNG)


5. In the allergy page, click “Add New Allergy” button to add a new allergy

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-02-05.PNG)


6. In the “comment” field, add the script (`<script>alert("Attacked")</script>`). Other field can be filled with own choice. After that, save the allergy.

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-02-06.PNG)


7. Go to the allergy page again to see if there is a pop-up with message "Attacked"


8. Again add a new allergy and In the “comment” field, add the script(`comment"><script>alert("Attacked")</script>`). Other field can be filled with own choice. After that, save the allergy.

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-02-07.PNG)


9. Go to the allergy page again to see if there is a pop-up with message "Attacked"


### * Expected results
1. Scripts are not accepted. No pop-up.
2. Scripts are accepted but not executed. No pop-up.

### * Actual results
Scripts are accepted but not executed. No pop-up.

![](https://github.com/genterist/openMRS-Security/blob/master/1-OWASP-Assesment/Test%20Step/A3-02-08.PNG)

### Test status : [ Pass ]