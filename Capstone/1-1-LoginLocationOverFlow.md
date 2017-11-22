## 1-1 LOGIN LOCATION OVERFLOW

### Affected module : OpenMRS login / Registration
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : Buffer overflow
+ Attack value : 99999999999999999999

### Bug Description
 When logging in, there was no safe failing mechanism for invalid selection of session location value. In this case, server prints out full stack trace of the error. One way to carry out this attack is through SQL injection and replace the values of all location IDs with values beyond the scope of integer. Sequential integer order of location ID is also vulnerable to location probing. For example, a clerk may not be able to see the locations accessible by the doctors from the UI but can try to manually probe the location by putting in the location ID. 

### Business impact
Attackers can cause this buffer overflow leading to a complete denial of service potentially to all system users. Depending on the scale and task, the cost of each downtime hour can range from $100 to thousands of dollars. Violation of Service Level Agreement regarding the uptime may also lead to legal issues and bad reputations. Further business plans that are based on the effectiveness of location tracking may be troubled. For example, if a hospital is planning on opening another hospital and thinking of establishing online boundaries between two hospitals by using the location feature, such plan will have to put on hold.

### Consequences
Denial of service on system like OpenMRS can cause severe consequences to all stakeholders. Patients will not be accepted as fast as the hospital can handle and it may be huge issues in emergency cases. Doctors unable to look up important patient information will further cause delays in treatments and might even lead to incorrect decisions. With sequential integer as location ID, malicious insiders can try and may successfully login to locations s/he is not supposed to be in.

### Mitigation
We proposed the short term fix and the long term fix.
The short term fix is to truncate the raw location ID string before converting it to integer to be used by other functions. This is one example of a possible fix
#### Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix1.png)
<br/>
#### Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix2.png)
<br/>
The long term fix is to establish a hash table, mapping hashed values with true location IDs and only the hash values are made viewable by the users. This reduces the chance of location hijacking and improves the security of all components that use location data. For example, there are some modules or some programs made available to some certain locations. Making location data harder to guess will also help security administrator spot issues quicker. For example, a particular user was logged in into 2 locations at the same time.



