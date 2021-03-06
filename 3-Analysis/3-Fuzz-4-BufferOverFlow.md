# Fuzz -4- LOGIN PAGE BUFFER OVER FLOW
### Priority : HIGH
### Test status : PASSED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Fuzz string : username=admin&password=[fuzz data]&sessionLocation=2&redirectUrl=
+ Fuzz data : jbrofuzz pre-installed rules in OWASP scanner
Fuzzer will deploy 17 buffer overflow attack strings on the variable "password" in form of POST requests. Server HttpResponses will be analyzed and be decided if the attacks were successful or not.


### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally

### * Test Data
jbrofuzz rules came standard with OWASP Zap

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open OWASP Zap V2.6.0
3. From OWASP Zap, go to Toos > Launch the Zap JxBrowser
4. In the Zap JxBrowser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
5. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the JzBrowser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

6. Go back to the Zap JxBrowser and type a bogus pair of username/password (we use "admin" for username and "BBBBB" for password), select "Pharmacy" section and click login. When the page got reloaded with "Invalid username/password. Please try again", close JxBrowser window and get back to main Zap window

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/adminLoginScreen.png)

7. In zap window, if you see "POST:login.htm(password, redirectURL,sessionLocation,username)" on the left panel (the "Sites" panel) then you got it, if not, please repeat step 3 to 5
8. Select "POST:login.htm(password, redirectURL,sessionLocation,username)" from the left panel and select the "Request" tab on the right panel. The right panel will turn into 2 smaller panels. At the bottom one, you will see "username=admin&password=BBBBB&sessionLocation=2&redirectUrl="
9. Highlight the "BBBBB" part from the string you got in previous step, right click on it and choose "Fuzz". A Fuzzer window will be opened.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/openFuzzMenu.png)

10. In the fuzzer window, click "Payloads..." button. A child window will be opened

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzerWindow.png)

11. In the child "Payloads" window, click "Add". An "Add payload" window will be opened
12. In "Add payload window, in the "Type" box, choose "File Fuzzers". Expand the "jbrofuzz" section. Check the box of "Buffer Overflow" and click "Add". The child window will be closed.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzBOF.png)

13. In Payloads window, click "OK" and you will be returned to the "Fuzzer" window. In this window, click "Start Fuzzer" button and you will be returned to the main Zap window with the "Fuzzer" tab selected
14. Observe the results in the "Fuzzer" tab, especially the "Code" and "Size Resp. Body". Check the HTTP response by selecting a fuzz entry, and select the "Response" tab in the uper right panel.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/BOFresults.png)

### * Expected results
+ OpenMRS should redirect invalid logins back to the login page.
+ System has to be able to fail securely.

### * Post-condition
OpenMRS should still be operating normally

### * Actual results
+ 17 fuzz were done on the "password" variable
+ All of the entries have 302 code and zero size of Response html body. Confirmed by inspection of html header, noticing that system redirects invalid login to previous page - the login page. 

### * NOTES:
In the future, we would create more fuzz cases with higher amount of characters 