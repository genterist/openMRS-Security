# PROTECTION TREE ANALYSIS OF OPENMRS - REGISTRATION MODULE

`AUTHOR : TAM N. NGUYEN` <br/>
`UPDATED ON : 05OCT2017` <br/>


## Description
This protection tree analysis focuses on the  OpenMRS' "Register a patient" (/openmrs/registrationapp/registerPatient.page?appId=referenceapplication.registrationapp.registerPatient) and "Find Patient Record" (/openmrs/coreapps/findpatient/findPatient.page?app=coreapps.findPatient). The purpose of this documentation is to evaluate briefly the probability and cost of some common defense mechanism. The tree creation was done from top down and evaluation was done from bottom up. This protection tree is for academic purposes and by no way should it be treated as a complete protection tree even for just this module.

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
Based on the above assumptions, we will use CVSS 3.0 calculator (https://www.first.org/cvss/calculator/3.0) to calculate the base threat probability. For example, if CVSS 3.0 score is 5, we will assume that the probability that the incident will happen is 50%. From the 11 criteria to decide the based threat score and base on the remedy options, we will lower the severity of each criteria. For example, if we believe the remedy option will lower a threat with "Confidentiality" risk of "High" to "None" then we will select "None". This will give us a new threat score under the effects of the remedy solution. We then use the formula : success proability = 1 - affected threat score. For example, if the base threat score is .7 and the new modified threat score is .5, the success probability of the remedy will be 1 - .5 = .5 

### Cost calculation
* We based our cost on W.H.O recommended cost for health care center cost in Kenya (http://www.who.int/choice/country/ken/cost/en/). We will go with the least cost, per 20 minutes for LCU which is $139 (a quantified unit with consideratios of many factors such as salaries, electricity, fuel, etc). For each type of threat, we will calculate the time needed for us to mitigate the threat. We then add 20% more time and use the final time value together with the above mentioned 20-min unit cost to calculate the final cost. This cost will be served as the MAXIMUM cost of the solution implying that the cost to prevent an issue should not greater than the cost to fix the issue.
* All of the costs at tree nodes do not include other indirect costs.


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
