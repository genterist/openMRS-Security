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
   
   a. Descriptions : with no account, attackers perform SQL injection attacks on login page and was able to extract all patient record
   
   b. Tools : SQLmap, SQLninja, SQLsus, Mole...
   
   c. Estimates
      * Probability
      * Cost
2. Java zero day
   
   a. Descriptions
   
   b. Tools
   
   c. Estimates
      * Probability
      * Cost
3. SQL zero day
   
   a. Descriptions
   
   b. Tools
   
   c. Estimates
      * Probability
      * Cost
4. Session hijacking
   
   a. Descriptions
   
   b. Tools
   
   c. Estimates
      * Probability
      * Cost
5. Man in the middle
   
   a. Descriptions
   
   b. Tools
   
   c. Estimates
      * Probability
      * Cost
6. Cross-site request forgery
   
   a. Descriptions
   
   b. Tools
   
   c. Estimates
      * Probability
      * Cost
7. Broken authentication
   
   a. Descriptions
   
   b. Tools
   
   c. Estimates
      * Probability
      * Cost
8. SQL injection
   
   a. Descriptions
   
   b. Tools
   
   c. Estimates
      * Probability
      * Cost
9. Underprotected API
   
   a. Descriptions
   
   b. Tools
   
   c. Estimates
      * Probability
      * Cost
      
10. Key logger
   
    a. Descriptions
   
    b. Tools
   
    c. Estimates
      * Probability
      * Cost
      
11. Send content to printer
   
    a. Descriptions
   
    b. Tools
   
    c. Estimates
      * Probability
      * Cost
      
12. Mirroring HDD
   
    a. Descriptions
   
    b. Tools
   
    c. Estimates
      * Probability
      * Cost
      
13. Memory dump
   
    a. Descriptions
   
    b. Tools
   
    c. Estimates
      * Probability
      * Cost
      
14. Buffer overflow
   
    a. Descriptions
   
    b. Tools
   
    c. Estimates
      * Probability
      * Cost
      
15. Direct copy of SQL files
   
    a. Descriptions
   
    b. Tools
   
    c. Estimates
      * Probability
      * Cost
      
16. Cache attack
   
    a. Descriptions
   
    b. Tools
   
    c. Estimates
      * Probability
      * Cost
      
17. Spyware/Trojan
   
    a. Descriptions
   
    b. Tools
   
    c. Estimates
      * Probability
      * Cost
      
18. Whaling
   
    a. Descriptions
   
    b. Tools
   
    c. Estimates
      * Probability
      * Cost
      
19. Shoulder surfing
   
    a. Descriptions
   
    b. Tools
   
    c. Estimates
      * Probability
      * Cost
      
20. Impersonation
   
    a. Descriptions
   
    b. Tools
   
    c. Estimates
      * Probability
      * Cost
