## 1-2 LOGIN PAGE REDIRECT TO LOGOUT 

### Affected module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : unauthorized redirect after login
+ Attack value : %2Fopenmrs-standalone%2Fappui%2Fheader%2Flogout.action%3FsuccessUrl%3Dopenmrs-standalone

### Bug Description
Attackers can redirect logged in users immediately to a logout page upon users' successful logon, creating an illusion that user's credential was not correct. The exploit is simple yet can cause a massive confusion as well as effective denial of service. In another case, attackers may redirect users to a malicious page upon login in order to steal session cookies and other important information.


### Business impact
Attackers can cause this buffer overflow leading to a complete denial of service potentially to all system users. Depending on the scale and task, the cost of each downtime hour can range from $100 to thousands of dollars. Violation of Service Level Agreement regarding the uptime may also lead to legal issues and bad reputations. Further business plans that are based on the effectiveness of location tracking may be troubled. For example, if a hospital is planning on opening another hospital and thinking of establishing online boundaries between two hospitals by using the location feature, such plan will have to put on hold.


### Consequences
Denial of service on system like OpenMRS can cause severe consequences to all stakeholders. Patients will not be accepted as fast as the hospital can handle and it may be huge issues in emergency cases. Doctors unable to look up important patient information will further cause delays in treatments and might even lead to incorrect decisions. With sequential integer as location ID, malicious insiders can try and may successfully login to locations s/he is not supposed to be in.

### Mitigation
We propose two solutions, one for short term and the other one for long term.
For the short term, the solution is to spot and replace any "logout" string with a "home" string so that even when attackers found a way to force the logout page (to accomplish denial of service), the server codes will change that and redirect user back to home.
#### Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix3.png)
<br/>
#### Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix4.png)
<br/>
For the long term solution, we recommend encryption of URL information. Before sending the responses to clients, the server encrypts the redirection URL using a private key. Later on, when receiving back the URL redirection data from client's request, server will decrypt and perform redirection. Due to encryption mechanism, it will be impossible for attackers to guess or forge redirection data. The private key can be deprived from the session key so we will have a new key for each user session.
