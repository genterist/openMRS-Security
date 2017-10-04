# ATTACK TREE ANALYSIS OF REGISTRATION MODULE

`AUTHOR : TAM N. NGUYEN` <br/>
`UPDATED ON : 01OCT2017` <br/>


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

### Cost calculation
* We based our cost on W.H.O recommended cost for health care center cost in Kenya (http://www.who.int/choice/country/ken/cost/en/). We will go with the least cost, per 20 minutes for LCU which is $139. For each type of threat, we will calculate the time needed for us ourselves to mitigate the threat. We then add 20% more time and use the final time value together with the above mentioned 20-min unit cost to calculate the final cost.
* All of the costs at tree nodes do not include the actual cost of patient record leak itself. In the case of Kenya, the cost for patient data leak may not be that high compared to that of the US. It is due to the legal obligations, laws, or even the nature of the clinic. If this is a non-profit clinic ran by W.H.O, there may be a clause saying that patients waive the rights in all legal cases before they are admitted to the clinic.

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
