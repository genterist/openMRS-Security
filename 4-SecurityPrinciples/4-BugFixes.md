# Client Bypass -1- LOGIN PAGE INTEGER BUFFER OVER FLOW

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : Buffer overflow
+ Attack value : 99999999999999999999
+ Location value was overflow leading to exposure of stack trace info


### * Bug Fix
####Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix1.png)
<br/>
####Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix2.png)
<br/>
We trim the raw location session string into 3 characters in length to avoid the overflow error when the program tries to cast the string into integer.


# Client Bypass -3- LOGIN PAGE REDIRECT

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : unauthorized redirect after login
+ Attack value : %2Fopenmrs-standalone%2Fappui%2Fheader%2Flogout.action%3FsuccessUrl%3Dopenmrs-standalone
In this test, we will redirect logged in user to a logout page, aiming for an illusion that user's credential was not correct. The exploit is simple yet can cause a massive confusion as well as effective denial of service

### * Bug Fix
####Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix3.png)
<br/>
####Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix4.png)
<br/>
We replace all referral URL value that containts "logout.page" and turn it into "home.page"


# Fortify analysis -2- COMMAND LINE INJECTION

### * Description
#### Name of module : OpenMRS login
The method execMysqlCmd() in MigrateDataSet.java:187 calls exec() with a command built from untrusted data. This call can cause the program to execute malicious commands on behalf of an attacker.

### * Bug Fix
####Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix5.png)
<br/>
####Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix6.png)
<br/>
Make the variable private and use a maping table to map certain whitelisted inputs to certain relevant database paramaters (table names, etc). The case in the screenshot is done by explicitly assign the database name to the variable. This warning is common in many files so it has to be up to each developer to do his/her own whitelisting


# Fortify analysis -3- PRIVACY VIOLATION

### * Description
#### Name of module : OpenMRS login
The method authenticate() in Context.java:287 mishandles confidential information, which can compromise user privacy and is often illegal. More specifically, the password enters the program, and the statement log.debug("Authenticating with username: " + username); in authenticate() will display the username in log when debug is enabled.

### * Bug Fix
####Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix7.png)
<br/>
####Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix8.png)
<br/>
Follow recommendations at https://wiki.openmrs.org/display/docs/Security+and+Encryption we encode the plain password using the built-in "encodeString" function. This change has to be made accross all authentication functions that use plain password as input.

# Fortify analysis -4- PASSWORD IN CONFIGURATION FILE

### * Description
#### Name of module : OpenMRS login
In liquibase-core-data.xml:5, the password is stored as plaintext in the configuration file. Storing a plaintext password in a configuration file may result in a system compromise.

### * Bug Fix
####Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix7.png)
<br/>
####Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix8.png)
<br/>
Follow recommendations at https://wiki.openmrs.org/display/docs/Security+and+Encryption we encode the plain password using the built-in "encodeString" function. This change has to be made accross all authentication functions that output password into XML files.
