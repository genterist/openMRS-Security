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
We based our cost on W.H.O recommended cost for health care center cost in Kenya (http://www.who.int/choice/country/ken/cost/en/). We will go with the least cost, per 20 minutes for LCU which is $139. For each type of threat, we will calculate the time needed for us ourselves to mitigate the threat. We then add 20% more time and use the final time value together with the above mentioned 20-min unit cost to calculate the final cost.

1. SQL Injection
   1. Descriptions : with no account, attackers perform SQL injection attacks on login page and was able to extract all patient record
   2. Tools : SQLmap, SQLninja, SQLsus, Mole...
   3. Estimates
      * Probability
      * Cost
2. Java zero day
   1. Descriptions
   2. Tools
   3. Estimates
      * a
3. SQL zero day
   1. Descriptions
   2. Tools
   3. Estimates
      * a
4. Session hijacking
   1. Descriptions
   2. Tools
   3. Estimates
      * a
5. Man in the middle
   1. Descriptions
   2. Tools
   3. Estimates
      * a
6. Cross-site request forgery
   1. Descriptions
   2. Tools
   3. Estimates
      * a
7. Broken authentication
   1. Descriptions
   2. Tools
   3. Estimates
      * a
8. SQL injection
   1. Descriptions
   2. Tools
   3. Estimates
      * a
9. Underprotected API
   1. Descriptions
   2. Tools
   3. Estimates
      * a
10.Key logger
   1. Descriptions
   2. Tools
   3. Estimates
      * a
11.Send content to printer
   1. Descriptions
   2. Tools
   3. Estimates
      * a
12.Mirroring HDD
   1. Descriptions
   2. Tools
   3. Estimates
      * a
13.Memory dump
   1. Descriptions
   2. Tools
   3. Estimates
      * a
14.Buffer overflow
   1. Descriptions
   2. Tools
   3. Estimates
      * a
15.Direct copy of SQL files
   1. Descriptions
   2. Tools
   3. Estimates
      * a
16.Cache attack
   1. Descriptions
   2. Tools
   3. Estimates
      * a
17.Spyware/Trojan
   1. Descriptions
   2. Tools
   3. Estimates
      * a
18.Whaling
   1. Descriptions
   2. Tools
   3. Estimates
      * a
19.Shoulder surfing
   1. Descriptions
   2. Tools
   3. Estimates
      * a
20.Impersonation
   1. Descriptions
   2. Tools
   3. Estimates
      * a
