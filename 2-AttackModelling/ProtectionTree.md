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

