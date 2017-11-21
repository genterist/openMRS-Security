# CSC 515 Project - Milestone 2 #

## 0. Module Selection ##

Registration Module

<br>

## 1. Password Strength ##

Since some of the content contains Chinese, we translated the Chinese reminding message into English using the translator( which is also showed in the picture).

### Minimum length : 8
![alt text](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/picture/length.PNG)

### Maximum length : none(5000 characters passed)
![alt text](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/picture/length2.PNG)

### Number of allowable characters: Required Upper and lower characters, at least on digit
![alt text](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/picture/3.PNG)
![alt text](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/picture/4.PNG)

### Allowable characters: all characters
![alt text](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/picture/5.PNG)

### Password reuse policy: You can reuse the old password, no specific policy.
![alt text](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/picture/6.PNG)

### Account lock out : Locked the 8th failed log in.

<br><br>

##  2. Abuse/Misuse Cases ##

### Diagram ###

![](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/Diagram.png)

### Abuse Case 1 ###

| Abuse Cases               | Content |
| :---						| :---    |
| Abuse Case ID 			| Registration-A1 |
| Abuse Case Name 			| Stored XSS Attack |
| Author					| Xiangqing Ding |
| Date						| 10/01/2017 |
| Actor						| (Malicious) Registration Clerk |
| Summary					| A registration clerk binds some malicious cross-site script when setting or editing patient's information. As a result, anyone who view the patient's page will suffer an XSS attack  |
| Basic Path				| BP0-1. The clerk logs into the openMRS system <br> BP0-2. The clerk goes to the patient registration page and registers a new patient <br> BP0-3. The clerk puts some XSS script in some information fields (like "address") of the new patient 	<br> BP0-4. After completing the registration form, the clerk clicks the confirmation button to finish registering the patient <br> BP0-5. Anyone that view the patient's information will be attacked |
| Alternative Paths			| AP0-1. The clerk logs into the openMRS system <br> AP0-2. (Change step BP0-2) The clerk goes to the search page and searches for an existing patient <br> AP0-3. (Change step BP0-3) The clerk edits the information of the existing patient and puts some XSS script in some information fields	<br> AP0-4. (Change step BP0-4) After completing the form, the clerk clicks the confirmation button to finish editing the patient information <br> AP0-5. Anyone that view the patient's information will be attacked | |
| Capture Points			| CP1: (For BP0-4) The script is not accepted. The clerk cannot create a user until the input is valid  <br> CP2: (For BP0-5) The script is accepted. But it cannot be executed for some mitigation techniques used in the system	|
| Extension Points			| N/A	|
| Preconditions				| 1. The system including registration module run well <br> 2. No other connection problems like network or database connection |
| Assumptions				| 1. The system is not guaranteed to be invulnerable to XSS attack (i.e. has corresponding mitigation or protection)  <br> 2. The process will not be interrupted by environment, like being found and stopped by other stuffs	|
| Worst case threat			| The malicious script is stored in the database and will be loaded when used. Anyone who visit the patient's page will suffer an XSS attack	|
| Capture Guaranteed		| The script is not accepted or doesn't work |
| Potential Misuse Profile 	| Skilled. The clerk should at least have some knowledge of web and XSS |
| Related Business Rules| BR1. System should adopt mitigation techniques to avoid being attacked <br> BR2. Access to private information should be restricted and logged |
| Stakeholder and Threats	| SH1: Employee: Employees who view the patient page will suffer XSS attack like session exposed <br> SH2: Hospital using this system: The reputation of the hospital will be damaged <br> SH3: Patient: With incorrect information, the patient may meet some problems like being unable to be contacted |
| Scope 					| Whole system |
| Abstraction level 		| Abuser goal  |
| Precision level 			| Focused |

 
### Abuse Case 2 ###

| Column                	| Content |
| :---						| :---    |
| Abuse Case ID 			| Registration-A2 |
| Abuse Case Name 			| Interpolating Patients' Information |
| Author					| Zhuo Li |
| Date						| 10/01/2017 |
| Actor						| (Malicious) Registration Clerk |
| Summary					| A registration clerk changes the information of patients for own purpose, without permission from other stuffs and notice to patients  |
| Basic Path				| BP0-1. The clerk logs into the openMRS system <br> BP0-2. The clerk searches the patient he/she wants to to interpolate, and then goes to the page of the patient <br> BP0-3. The clerk edits the information of the patient for own purpose <br> BP0-4. After completing the form, the clerk clicks the confirmation button to confirm the change <br> BP0-5. The patient information has been changed |
| Alternative Paths			| AP0-1. The clerk logs into the openMRS system <br> AP0-2. The clerk registers a new patient <br> AP0-3. (Change step BP0-3) The clerk interpolates the information of the patient for own purpose <br> AP0-4. After completing the registration form, the clerk clicks the confirmation button to confirm the registration <br> AP0-5. The interpolated patient information has been changed |
| Capture Points			| CP1: (For BP0-4) The clerk needs permission to change the information of patients	|
| Extension Points			| EP1: Include misuse case "Stored XSS Attack" (In BP0-3) |
| Preconditions				| 1. The system including registration module run well <br> 2. No other connection problems like network or database connection |
| Assumptions				| The process will not be interrupted by environment, like being found and stopped by other stuffs	|
| Worst case threat			| The information of patient has been successfully changed. No one discovers this problem.	|
| Capture Guaranteed		| The clerk cannot change information of patient without permission. The integrity of patient information is guaranteed |
| Potential Misuse Profile 	| Common. Knowing how to operate openMRS is enough |
| Related Business Rules	| BR1. Access to private information should be restricted and logged |
| Stakeholder and Threats	| SH1: Employee: Employees who use the wrong patient information may cause some problem and thus be punished <br> SH2: Hospital using this system: The reputation of the hospital will be damaged <br> SH3: Patient: With incorrect information, the patient may meet some problems like being unable to be contacted	|
| Scope 					| Whole system |
| Abstraction Level 		| Abuser goal  |
| Precision level 			| Focused 	   |


### Misuse Case 1 ###

| Column                	| Content |
| :---						| :---    |
| Misuse Case ID 			| Registration-M1 |
| Misuse Case Name 			| Registering Duplicate Patient |
| Author					| Fuxing Luan |
| Date						| 10/01/2017 |
| Actor						| (Careless) Registration Clerk |
| Summary					| A registration clerk unintentionally registers the patient twice or more times, causing a redundancy in system database and other problems |
| Basic Path				| BP0-1. The clerk logs into the openMRS system <br> BP0-2. The clerk goes into the registration page for registering new patient <br> BP0-3. For some reason, the clerk unintentionally creates the patient twice or more times  <br> BP0-4. Two or more information entries for the same patient are stored in the system database |
| Alternative Paths			| N/A |
| Capture Points			| CP1: (For BP0-4) The system will found out duplicate patient information and prevents the registration or sends check notice with the clerk <br> CP2: Anyone found the error and reported it to the administrator. The administrator manually deletes the duplicate information entry	|
| Extension Points			| N/A	|
| Preconditions				| 1. The system including registration module run well <br> 2. No other connection problems like network or database connection  |
| Assumptions				| The process will not be interrupted by environment, like being found and stopped by other stuff	|
| Worst case threat			| The real patient is hard to find in the system 	|
| Capture Guaranteed		| The clerk should double check the information that he inputs |
| Potential Misuse Profile 	| Common |
| Related Business Rules	| BR1. System should support functions of correcting operation error |
| Stakeholder and Threats	| SH1: Employee: Employees will be confused about the duplicate patient information. Both may need to be updated when patient information changing <br> SH2: Hospital using this system: The reputation of the hospital will be damaged |
| Scope 					| Whole system 	|
| Abstraction Level 		| Misuser goal  |
| Precision level 			| Focused 		|


### Misuse Case 2 ###

| Column                	| Content |
| :---						| :---    |
| Misuse Case ID 			| Registration-M2 |
| Misuse Case Name 			| Wrong Information Provided by Patient  |
| Author					| Tam Nguyen |
| Date						| 10/01/2017 |
| Actor						| (Forgetful) Patient |
| Summary					| A patient provides wrong information to the registration clerk during registration  |
| Basic Path				| BP0-1. The patient requests for being registered to the system <br> BP0-2. During the registration, the patient provides some wrong information, like wrong phone number, to the clerk <br> BP0-3.The patient is registered with wrong information |
| Alternative Paths			| N/A |
| Capture Points			| CP1: (For BP0-2) The clerk double checks the information provided by the patient and corrects the error <br> CP2: (For BP0-2)The patient recalls the correct information and gives clerk the right one <br> CP3: After registration, the patient recalls the correct information and asks clerks to correct it |
| Extension Points			| N/A	|
| Preconditions				| 1. The system including registration module run well <br> 2. No other connection problems like network or database connection  |
| Assumptions				| The process will not be interrupted by environment, like being found and stopped by other stuff	|
| Worst case threat			| The wrong patient information is created and used |
| Capture Guaranteed		| The wrong information is corrected during or after the registration, and not be used by anyone |
| Potential Misuse Profile 	| Common |
| Related Business Rules	| BR1. System should support functions of changing incorrect data <br> BR2. Employee should validate the data being recorded into the system  |
| Stakeholder and Threats	| SH1: Employees who use the wrong patient information may cause some problem and thus be punished <br> SH2: Hospital using this system: The hospital may suffer accident caused by wrong patient information <br> SH3: Patient: With incorrect information, the patient may meet some problems like being unable to be contacted	|
| Scope 					| Whole system |
| Abstraction Level 		| Misuser goal  |
| Precision level 			| Focused |


<br><br>

##  3. Attack Trees and Protection Trees ##


## Description
This attack tree analysis focuses on the  OpenMRS' "Register a patient" (/openmrs/registrationapp/registerPatient.page?appId=referenceapplication.registrationapp.registerPatient) and "Find Patient Record" (/openmrs/coreapps/findpatient/findPatient.page?app=coreapps.findPatient). The purpose of this documentation is to evaluate briefly the probability and cost of some common attack paths. The tree creation was done from top down and evaluation was done from bottom up.

## ASSUMPTIONS
* We assume OpenMRS used is a standalone version installed on a desktop. This fits the major user base that OpenMRS target - small scale clinic in underdeveloped areas.
* We assume there is just a small local network among local computers with no access to the Internet
* We assume the clinic members have overlapped roles such as a nurse may have to perform the tasks of a clerk sometimes.
* We assume the physical security of the place is less than American's standards (no ID activated doors, no armed guards)
* We assume the computer is used for more than just one purpose of hosting the local version of OpenMRS.
* We assume several staff members can use the computer per day
* We assume system support personel had enough training and capability to troubleshoot and remedy all issues relating to the system
* We assume system support personels are not onsite and we will use 20% rule as added time on top of time required to solve any case

## METRICS
### Probability calculation
Based on the above assumptions, we will use CVSS 3.0 calculator (https://www.first.org/cvss/calculator/3.0) to calculate the base probability. For example, if CVSS 3.0 score is 5, we will assume that the probability that the incident will happen is 50%. While CVSS score does not directly translate to threat probability in real life, for this project, we believe it is strong enough to be based on since it involves 11 groups of parameters (parameter groups in base score and temporal score)

### Cost calculation for attack tree
* We based our base cost on W.H.O recommended cost for health care center cost in Kenya (http://www.who.int/choice/country/ken/cost/en/). We will go with the least cost, per 20 minutes for LCU which is $139. For each type of threat, we will calculate the time needed for us ourselves to mitigate the threat. We then add 20% more time and use the final time value together with the above mentioned 20-min unit cost to calculate the final base cost. All money values in the tree are base costs 
* On top of the base costs, the actual money benefited from exploiting the patient records can be added. For example, if the attackers think they can "sell" the patient records to someone for $20000 then a reasonable amount of total cost for an exploit should be 50% of $20000 plus the base cost. Because it is extremely hard to predict how a particular group of attackers will benefit from their hacking works, we do not attempt to calculate the final cost. The idea is the attacker should not invest more on an exploit than the ROI (return of investment) from an exploit.

### Cost calculation for protection tree
* We based our cost on W.H.O recommended cost for health care center cost in Kenya (http://www.who.int/choice/country/ken/cost/en/). We will go with the least cost, per 20 minutes for LCU which is $139 (a quantified unit with consideratios of many factors such as salaries, electricity, fuel, etc). For each type of threat, we will calculate the time needed for us to mitigate the threat. We then add 20% more time and use the final time value together with the above mentioned 20-min unit cost to calculate the final cost. This cost will be served as the MAXIMUM cost of the solution implying that the cost to prevent an issue should not greater than the cost to fix the issue.
* All of the costs at tree nodes do not include other indirect costs.

### Impact calculate
We calculate impact based on these ranges

1-3 : Minor

4-6 : Moderate

7-9 : Significant

10 : Total impact

### Risk calculation
We calculate risks on leaf nodes based on this equation

risk = (probability/cost) * impact

### Propogation of metrics

![Propagation](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/picture/Propagation.png?raw=true)

### Attack tree leaf description

1. SQL Injection
   
   a. Descriptions : with no account, attackers perform SQL injection attacks on login page and was able to extract all patient records. From failed login logs, this type of attack can be quickly identified (identification time = 20 minutes). Attack string might be recorded in logs. Only work-around can be provided such as adding another layer of authentication provided by Apache TomCat for that specific page (40 minutes).
   
   b. Tools : SQLmap, SQLninja, SQLsus, Mole...
   
   c. Estimates
      * Probability : 60%
      * Cost: (60*1.2)/20 * 139 = $500
      
2. Java zero day
   
   a. Descriptions : with no account, attacker exploited Java server zero day vulnerability to create a backdoor. Exploit has to be performed on the computer that hosts OpenMRS. Because this may not directly create any OpenMRS log, it may take a while to be fully identified. The only work around is to reinstall java JRE and install host intrusion prevention system with ability to monitor changes to JRE files, and even JRE real time processes.
   
   b. Tools: strace, ltrace, ADA, other reverse engineer tools, other ROP tools, ...
   
   c. Estimates
      * Probability: 43%
      * Cost : (300*1.2)/20 * 139 = $2500
      
3. SQL zero day
   
   a. Descriptionswith no account, attacker exploited SQL server zero day vulnerability to create a backdoor. Exploit has to be performed on the computer that hosts OpenMRS. Because this may not directly create any OpenMRS log, it may take a while to be fully identified. The only work around is to reinstall SQL and install host intrusion prevention system with ability to monitor changes to SQL files, and even SQL real time processes.
   
   b. Tools: strace, ltrace, ADA, other reverse engineer tools, other ROP tools, ...
   
   c. Estimates
      * Probability: 40%
      * Cost : (300*1.2)/20 * 139 = $2500
      
4. Session hijacking
   
   a. Descriptions: attacker from the clinic's local network hijacked an admin session by sniffing and replaying some network traffics. Inspecting network traffics (1 hour) will help identify the attacker and setting up HTTPs for the site (40 minutes) will help prevent the vulnerability.
   
   b. Tools: cookieCatcher, FireSheep, Juggernaut,...
   
   c. Estimates
      * Probability: 76%
      * Cost: ( 100 *1.2)/20 *139 = $834
      
5. Man in the browser
   
   a. Descriptions: attacker installed a mallicious browser plugin that secretly recorded all data sent between the server and the browser under admin sesssions. Recorded data got stored on local HDD or a local network drive. Mallicious plugin can be identified upon inspection (1 hour)
   
   b. Tools : mallicious extensions, API-hooking,...
   
   c. Estimates
      * Probability: 45%
      * Cost: ( 60*1.2)/20 *139 = $500
      
6. Cross-site request forgery
   
   a. Descriptions: attacker crafted a mallicious website that will query the database for full patient list under logged on OpenMRS admin session. Since we assume the Desktop is rarely connected to the internet and uses are strictly for the local clinic, the probability for this kind of attack is low. Network firewall log inspection will reveal the mallicious http requests and can be permanently fixed by whitelisting rules at gateway.
   
   b. Tools: OWASP scanner, BurpSuite, any html editor
   
   c. Estimates
      * Probability: 35%
      * Cost ( 60*1.2)/20 *139 = $500
      
7. Broken authentication
   
   a. Descriptions: a mallicious indider was able to predict the session ID generation rules and adjusted his/her regular session (with no read patient privilege) to a session with higher privilege. Inspecting login sessions and network logs may reveal inconsistencies in sessions. 
   
   b. Tools: any http header sniff and analyzer, built-in browser developer tool, some cryptography cracking tools, ...
   
   c. Estimates
      * Probability: 44%
      * Cost ( 120*1.2)/20 *139 = $1000
      
8. SQL injection
   
   a. Descriptions: a mallicious indider with no patient record read privilege was able to perform SQL injection on other forms and gained access to full list of patients. Inspecting network logs may reveal suspicious http requests.
   
   b. Tools : SQLmap, SQLninja, SQLsus, Mole...
   
   c. Estimates
      * Probability : 70%
      * Cost: (60*1.2)/20 * 139 = $500
      
9. Underprotected API
   
   a. Descriptions: a mallicious insider with no patient record read privilege was able to exploit bugs in API (either native or third party) and made the API to display full list of patients. Inspecting network logs may reveal suspicious http requests.
   
   b. Tools: any http header sniff and analyzer, built-in browser developer tool, portable fuzzer tools ...
   
   c. Estimates
      * Probability: 50%
      * Cost ( 60*1.2)/20 *139 = $500
      
10. Key logger
   
    a. Descriptions: attacker was able to install a keylogger on the local machine and record all key strokes including new patient data input and login credentials of all users using the workstation. Inspecting running processes and performing comprehensive scan may help identify and resolving the problem (2 hours)
   
    b. Tools: keylogger hardwares, keylogger software
   
    c. Estimates
      * Probability: 90%
      * Cost (120 *1.2)/20 *139 = $1000
      
11. Send content to printer
   
    a. Descriptions: attacker was able to install a script that will secretly send the content of a target page (patient list page) to a local network printer whenever a legitimate user browses to those certain pages. Over the time, attacker will have a decent list of all patients in the system. Inspecting print spooler requests will revleal the exploit.
   
    b. Tools: vbscript, shell script, batch script
   
    c. Estimates
      * Probability: 55%
      * Cost ( 60*1.2)/20 *139 = $500
      
12. Mirroring HDD
   
    a. Descriptions: attacker was able to use built in Raid mirroring functionality supported by the workstation and secretly installed additional HDDs, able to get the mirror of all main HDDs data and secretly harvest the mallicious HDD at a later time. Inspecting raid settings, physical inspection of hardware, physical security will help identify and mitigate the problem.
   
    b. Tools: existing hardware raid supports, existing software raid support
   
    c. Estimates
      * Probability: 45%
      * Cost (60*1.2)/20 *139 = $500
      
13. Memory dump
   
    a. Descriptions: attacker was able to secretly dump contents in memory into local disk or a local network location. Over the time, attacker can get login credentials, and browser contents including patient records. Process analysis, system call monitoring, antivirus scan may help identify and mitigate the problem.
   
    b. Tools: Live RAM Caputer, WindowsScope, Memoryze, trojans,...
   
    c. Estimates
      * Probability: 42%
      * Cost ( 100*1.2)/20 *139 = $834
      
14. Buffer overflow
   
    a. Descriptions: attacker caused a buffer overflow to execute payloads that affect OpenMRS, JDK, MySQL, browser, or flash and other plugins, leading to total exposure of patient info. System may or may not record the buffer overflow. Checking application log may reveal attempts.
   
    b. Tools: binary reverse engineering tools, payload preparation platforms, ROP tools, ...
   
    c. Estimates
      * Probability: 49%
      * Cost ( 400 *1.2)/20 *139 = $3336
      
15. Rootkit
   
    a. Descriptions: Attacker was able to install RootKit on the workstation that host the OpenMRS server and has total control. Identify and re-imaging the workstation will cost 3 hours at minimum.
   
    b. Tools: DerStarke, QuarkMatter, ...
   
    c. Estimates
      * Probability: 66%
      * Cost ( 180*1.2)/20 *139 = $1501
      
16. Cache attack
   
    a. Descriptions: Attacker was able to grab cached files produce by the system, or by OpenMRS and extract patient information from it. Under-protected SQL backups are also succeptible to this kind of attack.
   
    b. Tools: thumb drive to copy files, cryptanalysis tool, text extract tool, etc.
   
    c. Estimates
      * Probability: 37%
      * Cost ( 60*1.2)/20 *139 = $500
      
17. Spyware/Trojan
   
    a. Descriptions: attacker was able to plant a trojan or spyware on the computer and able to harvest all information, regarding login credentials
   
    b. Tools: Frog Prince, Grasshopper, CandyMountain, Assasin, ...
   
    c. Estimates
      * Probability: 61%
      * Cost ( 120*1.2)/20 *139 = $1000
      
18. Whaling
   
    a. Descriptions: attacker target key personel with high privilege and persuaded such people to execute a mallicious payload leading to attacker's total access to patient info.
   
    b. Tools: email with payload, social engineering over the phone, ...
   
    c. Estimates
      * Probability: 85%
      * Cost ( 60*1.2)/20 *139 = $500
      
19. Shoulder surfing
   
    a. Descriptions: attacker look over the shoulder or found a way to record an admin typing a password. This is a huge possibility considering the clinic is small, with low level of physical security.
   
    b. Tools: human eyes, secret cameras
   
    c. Estimates
      * Probability: 90%
      * Cost ( 180*1.2)/20 *139 = $1501
      
20. Impersonation
   
    a. Descriptions: attacker calls in or physically present and pretend to be soneone important and demand full list of patient.
   
    b. Tools: phone, physical appearance, social engineering
   
    c. Estimates
      * Probability: 65%
      * Cost ( 180*1.2)/20 *139 = $1501
      
 ### The attack tree
      
![Attack tree](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/OpenMRS-AttackTree.png?raw=true)

### Protection tree leaf descriptions

1. Proper loggin
   
   a. Descriptions : make sure all log functions from Apache TomCat, SQL, and OpenMRS itself are enabled. Test and make sure all less-than-desirable events are logged. Make sure events are generated correctly - for example, if it should be a 404 error, it should be a 404 error rather than a 200.
   
   b. Tools : all standard log monitor/generator tools
   
   c. Estimates
      * Probability : 65%
      * Cost: (60*1.2)/20 * 139 = $500
      
2. Avoid JAVA zero day attacks
   
   a. Descriptions : Follow and monitor threat networks like Cisco TALOS, the NVD for newly discovered Java vulnerabilities. Update JDK as soon as possible. Host based IPS with anomaly capability installed on OpenMRS host computer may also help
   
   b. Tools: HIPS with anomaly detection capabilities, threat intelligence networks ...
   
   c. Estimates
      * Probability: 75%
      * Cost : (300*1.2)/20 * 139 = $2500
      
3. Avoid mySQL zero day attacks
   
   a. Descriptions: Follow and monitor threat networks like Cisco TALOS, the NVD for newly discovered Java vulnerabilities. Update mySQL as soon as possible. Host based IPS with anomaly capability installed on OpenMRS host computer may also help
   
   b. Tools: HIPS with anomaly detection capabilities, threat intelligence networks ...
   
   c. Estimates
      * Probability: 75%
      * Cost : (300*1.2)/20 * 139 = $2500
      
4. Strict session control
   
   a. Descriptions: make sure the randomizer is good random, use a short window for sessions, only transmit session cookies over encrypted chanel.
   
   b. Estimates
      * Probability: 85%
      * Cost: ( 100 *1.2)/20 *139 = $834
      
5. Prevent Man in the browser
   
   a. Descriptions: user a network based IPS, host based IPS, application firewall
   
   b. Tools : HIPS, network IPS, antivirus
   
   c. Estimates
      * Probability: 75%
      * Cost: ( 60*1.2)/20 *139 = $500 (not counting the cost of hardwares)
      
6. Cross-site request forgery
   
   a. Descriptions:  using firewalls to whitelist websites - only a very few, work related websites will be allowed. This will help protect against CSRF.
   
   b. Tools: HIPS, network IPS, Firewalls
   
   c. Estimates
      * Probability: 35%
      * Cost ( 60*1.2)/20 *139 = $500
      
7. Folow NIST recommendations for authentications
   
   a. Descriptions: Following NIST's recommendations to implement correctly authentication schemes and prevent situations like a mallicious indider was able to predict the session ID generation rules and adjusted his/her regular session (with no read patient privilege) to a session with higher privilege.
   
   b. Tools: NIST recommendations, existing time-tested solutions ...
   
   c. Estimates
      * Probability: 44%
      * Cost ( 120*1.2)/20 *139 = $1000
      
8. Input sanitization
   
   a. Descriptions: Sanitize inputs and put restrictions on inputs. This will prevent situations like a mallicious indider with no patient record read privilege was able to perform SQL injection on other forms and gained access to full list of patients.
   
   b. Tools : existing time-tested input validation solutions...
   
   c. Estimates
      * Probability : 70%
      * Cost: (60*1.2)/20 * 139 = $500
      
9. Fuzz test the APIs
   
   a. Descriptions: Use an fuzzer like OWASP fuzz or test cases to fuzz the APIs to make sure there is no detectable vulnerability. This will prevent situations like a mallicious insider with no patient record read privilege was able to exploit bugs in API (either native or third party) and made the API to display full list of patients.
   
   b. Tools: any http header sniff and analyzer, built-in browser developer tool, portable fuzzer tools ...
   
   c. Estimates
      * Probability: 70%
      * Cost ( 60*1.2)/20 *139 = $500
      
10. Physical inspection of hardware
   
    a. Descriptions: Physically inspect hardwares and look for un-authorized devices such as unauthorized keyboards, unauthorized USB. This will prevent situations like an attacker was able to install a keylogger on the local machine and record all key strokes including new patient data input and login credentials of all users using the workstation.
   
    b. Tools: keylogger hardwares, keylogger software
   
    c. Estimates
      * Probability: 60%
      * Cost (120 *1.2)/20 *139 = $1000
      
11. Print-job authentication
   
    a. Descriptions: Requires re-authentication for all print jobs, making sure that it was the right person with the right reason to print the data out. This will prevent situations like an attacker was able to install a script that will secretly send the content of a loaded page (patient list page) to a local network printer whenever a legitimate user browses to the page.
   
    b. Tools: third-party softwares that control print spooler
   
    c. Estimates
      * Probability: 85%
      * Cost ( 60*1.2)/20 *139 = $500
      
12. Whole disk encryption
   
    a. Descriptions: Encrypt the whole disk system. This will prevent situations like an attacker was able to use built in Raid mirroring functionality supported by the workstation and secretly installed additional HDDs, able to get the mirror of all main HDDs data and secretly harvest the mallicious HDD at a later time.
   
    b. Tools: BitLocker or similar solutions
   
    c. Estimates
      * Probability: 95%
      * Cost (60*1.2)/20 *139 = $500
      
13. Force safe reboot after crash
   
    a. Descriptions: Force safe reboot after a system crash and require the attention of admin. This will prevent situations like an attacker was able to dump contents in memory into local disk and collect it for later analysis.
   
    b. Tools: Safemode in windows, group policy settings,...
   
    c. Estimates
      * Probability: 82%
      * Cost ( 100*1.2)/20 *139 = $834
      
14. Sandboxing
   
    a. Descriptions: Run the whole OpenMRS in a container with just enough resources for the software to run efficiently. This will prevent situations like an attacker caused a buffer overflow to execute payloads that affect OpenMRS, JDK, MySQL, browser, or flash and other plugins, leading to total exposure of patient info.
   
    b. Tools: Docker, Hadoop, CloudFoundry ...
   
    c. Estimates
      * Probability: 89%
      * Cost ( 400 *1.2)/20 *139 = $3336
      
15. Safeboot with BIOS check
   
    a. Descriptions: Use BIOS UEFI to check the MBR before booting. This will prevent situations like an attacker was able to install RootKit on the workstation that host the OpenMRS server and has total control.
   
    b. Tools: bios UEFI ...
   
    c. Estimates
      * Probability: 86%
      * Cost ( 180*1.2)/20 *139 = $1501
      
16. Access Control List with strict policies
   
    a. Descriptions: Use ACLs and policies to only allow the right people access to the right resources. This will prevent situations like an attacker was able to grab cached files produce by the system and extract patient information from it.
   
    b. Tools: Active Directory group policy and permissions, etc.
   
    c. Estimates
      * Probability: 97%
      * Cost ( 60*1.2)/20 *139 = $500
      
17. Host-based Intrusion Prevention System
   
    a. Descriptions: Use a HIPS to prevent situations like an attacker was able to plant a trojan or spyware on the computer and able to harvest all information, regarding login credentials
   
    b. Tools: McAffee, Norton, ...
   
    c. Estimates
      * Probability: 80%
      * Cost ( 120*1.2)/20 *139 = $1000
      
18. Enforce email signatures
   
    a. Descriptions: Making sure all work related emails are signed and encourage people to only open files from the people they trust and from signed emails. This will prevent situations like an attacker targeted key personel with high privilege and persuaded such people to execute a mallicious payload leading to attacker's total access to patient info.
   
    b. Tools: email signatures with public keys...
   
    c. Estimates
      * Probability: 85%
      * Cost ( 60*1.2)/20 *139 = $500
      
19. Improve physical security
   
    a. Descriptions: Improving physical security by placing security filter screen over monitor screen, secure placement of work stations, and mindful security guards. This will prevent situations like an attacker looked over the shoulder or found a way to record an admin typing a password.
   
    b. Estimates
      * Probability: 90%
      * Cost ( 180*1.2)/20 *139 = $1501
      
20. Cyber Awareness Training
   
    a. Descriptions: Conduct cyber awareness training and prevent situations like an attacker calls in or is physically present and pretend to be soneone important and demands full list of patients.
   
    b. Tools: online training, actual training
   
    c. Estimates
      * Probability: 65%
      * Cost ( 180*1.2)/20 *139 = $1501
      
 ### The protection tree
 
 ![The protection tree](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/OpenMRS-ProtectionTree.png?raw=true)
<br><br>

##  4. Vulnerability History ##

### Description
OpenMrs used to have XSS, CSRF and XXE Injection.

* (XSS and CSRF)Parameters that are displayed back to the user are mostly vulnerable to cross-site scripting as user input was not validate properly and as a result, the malicious script was stored by the application and executed when it was displayed back to the user.
* (XEE Injection)The vulnerability is caused due to an error when parsing XML entities within ZIP archives and can be exploited to e.g. disclose data from local resources or cause a DoS condition (billion laughs) via a specially crafted XML file including external entity references.
* (XSS)OpenMRS suffers from multiple stored and reflected cross-site scripting vulnerabilities when input passed via several parameters to several scripts is not properly sanitized before being returned to the user. This can be exploited to execute arbitrary HTML and script code in a user's browser session in context of an affected site.

### URL and evidence  
URL:
* https://www.cvedetails.com/vulnerability-list/vendor_id-14221/product_id-29315/Openmrs-Openmrs.html
![alt text](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/picture/7.PNG)

* https://packetstormsecurity.com/files/128748/OpenMRS-2.1-Access-Bypass-XSS-CSRF.html
![alt text](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/picture/8.PNG)

* https://packetstormsecurity.com/files/134700/OpenMRS-2.3-1.11.4-XXE-Injection.html
![alt text](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/picture/9.PNG)

* https://packetstormsecurity.com/files/134698/OpenMRS-2.3-1.11.4-Cross-Site-Scripting.html
![alt text](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/picture/10.PNG)

It’s found by the provided URL. We first search by google if there is any vulnerability history with openMRS vulnerability and found there are some( the first curl). Then we use packet storm to find the details.

## Are these commonly-occurring vulnerabilities?
Yes, these are commonly-occurring vulnerabilities. Because most of the application should have a log in and registration process. Mostly, the application focused on the log in part and ignore other important part such as registration.
Also, most application contain XML entities, most of them only check the grammar or syntax of the XML, they failed to check if this is a crafted XML including external entity references which can be used by hacker.

## How do you think OpenMRS had to fix the vulnerability?
The application should not only focus on the log in part but also everywhere of the system. There should be filter and checking part before and after every options to hide useless data and protect changed data. Moreover, before starting the whole system, there also should be some checking part to see if every file is safe and authenticated.

