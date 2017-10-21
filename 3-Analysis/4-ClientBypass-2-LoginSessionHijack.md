# Client Bypass -1- LOGIN PAGE SESSION HIJACK
### Priority : HIGH
### Test status : PASSED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : Session hijacking
+ Attack value : the JSESSIONID value of a user's session
This attack will try to swith the sessions between a clerk with limitted privilege and an administrator. Action is simple and based on modification of http header value.

### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally
3. OWASP Local Proxy was properly configured
4. Browser proxy setting was properly configured to be pointed to OWASP proxy

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open Google Chrome. In the browser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
3. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the Chrome browser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly. If the page is loaded, you need to make sure proxy settings on both OpenMRS and Google Chrome were configured properly.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

4. Go back to the Chrome and login with a pair of username/password (we use "admin" for username and "Admin123" for password), select "Pharmacy" section and click login. After successful login, you log out.
5. Repeat step 2 to 4 but with this URL "http://localhost:8081/openmrs-standalone/referenceapplication/login.page"

6. In zap window, if you see two important page staring with "POST:login.htm" and "POST:login.page" on the left panel (the "Sites" panel).

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sites.png)

7. Select "POST:login.htm(password, redirectURL,sessionLocation,username)" from the left panel and select the "Break..." and then click "Save" and do the same for the page starts with "POST:login.page" under "referenceapplication" folder. 
8. The "Break Points" tab in the bottom pane should look like this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/breakpoints-login.png)

9. We now get back to our browser. Go to "Settings" > "Clear browsing data". Choose "Clear the following items from the beginning of time", check all the boxes and click "Clear browsing data"
10. Close "Settings" tab, and refresh the OpenMRS login page. Type in username: admin, and password: Admin123, choose "Pharmacy" location and click "Login"
10. You will not be able to login right away and OWASP Zap proxy may issue you an alert saying it is interupting the request. In such case, you can acknowledge the alert. Your screen should look similar to this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup1.png)

11. Notice that by the end of the header, we have a value set of 
> Cookie: JSESSIONID=D1392D7F2D37E5208D57E0F677CBC686; referenceapplication.lastSessionLocation=2
Copy the value of JSESSIONID. Your value may be different and for our test at this time, that value is D1392D7F2D37E5208D57E0F677CBC686
12. Click the "play" button several more times until the browser finishes loading and you should be able to logged into the dashboard.
13. Keep the current browser window and open another Google Chrome browser window in ICOGNITO mode and go to the login page. You may have to click the play button several times for the page to load. Once the page is load, login with the clerk credential (Username: clerk, password: Clerk123) and location is "Registration Desk"
14. Notice that after you click "Login", you will be brought to OWASP Zap proxy and see something like this

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup2.png)

15. Replace the current value of JSESSIONID (highlighted in the screenshot) with the value of the other JSESSIONID which is in our case, the value in step 11. Click the play button after you're done.
16. Click play two more times and you will see another header with the variable JSESSIONID again.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup3.png)

Replace it again with the value you recorded in step 11 and then click play button.
17. The server will refuse and force the original sessionID value of clerk. If we keep changing the clerk's sessionID to the admin's sessionID, we will run into step 16 and loop in it again and again. If we accept the server's value of sessionID, after clicking the play button, we will return back to the login page with no account logged in. Note that this is within the Icognito browser. Admin is still logged in in the regular browser
18. Close the incognito browser. Log out of admin account in the regular browser (once again, you may to click the play button several times to log out)

### * Expected results
+ OpenMRS should fail securely either by issuing an error message or redirecting user to login page
+ Error should not reveal too much information about the system

### * Post-condition
OpenMRS should still be operating normally

### * Actual results
System silently redirect user to login page without any error or announcement.

### * NOTES:
n/a