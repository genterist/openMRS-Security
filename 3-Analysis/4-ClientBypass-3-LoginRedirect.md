# Client Bypass -3- LOGIN PAGE REDIRECT
### Priority : HIGH
### Test status : FAILED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : unauthorized redirect after login
+ Attack value : %2Fopenmrs-standalone%2Fappui%2Fheader%2Flogout.action%3FsuccessUrl%3Dopenmrs-standalone
In this test, we will redirect logged in user to a logout page, aiming for an illusion that user's credential was not correct. The exploit is simple yet can cause a massive confusion as well as effective denial of service


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

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/interup4.png)

11. Notice that in the request body, there is a variable "redirectUrl" (the highlighted section). We will replace the value of that variable with "%2Fopenmrs-standalone%2Fappui%2Fheader%2Flogout.action%3FsuccessUrl%3Dopenmrs-standalone" (no double quotes) and then click the "play" symbol right above the "request" tab

12. Click the "play" button several more times until the browser finishes loading and we will find that we are at the login page (as if our login credential used was not correct)


### * Expected results
+ OpenMRS should recognize the erronous flow and correct it by defaulting it to a page other than the logout page and still log user in correctly.

### * Post-condition
OpenMRS should still be operating normally

### * Actual results

User was returned to the login page as if the login credential was not correct

### * NOTES:
n/a