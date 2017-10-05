#  Abuse/Misuse Cases #

## Diagram ##

![](https://github.com/genterist/openMRS-Security/blob/master/2-AttackModelling/Diagram.png)

## Abuse Case 1 ##

| Abuse Cases               | Content |
| :---						| :---    |
| Abuse Case ID 			| Registration-A1 |
| Abuse Case Name 			| Stored XSS Attack |
| Author					| Xiangqing Ding |
| Date						| 10/01/2017 |
| Actor						| (Malicious) Registration Clerk |
| Summary					| A registration clerk binds some malicious cross-site script when setting or editing patient's information. As a result, anyone who view the patient's page will suffer an XSS attack  |
| Basic Path				| BP0-1. The clerk logs into the openMRS system <br> BP0-2. The clerk goes to the patient registration page and registers a new patient <br> BP0-3. The clerk puts some XSS script in some information fields (like "address") of the new patient 	<br> BP0-4. After completing the registration form, the clerk clicks the confirmation button to finish registering the patient <br> BP0-5. Anyone that view the patient's information will be attacked |
| Alternative Paths			| AP0-1. The clerk logs into the openMRS system <br> AP0-2. (Change step BP0-2) The clerk goes to the search page and searches for an existing patient <br> AP0-3. (Change step BP0-3) The clerk edits the information of the existing patient and puts some XSS script in some information fields	<br> AP0-4.(Change step BP0-4) After completing the form, the clerk clicks the confirmation button to finish editing the patient information <br> AP0-5. Anyone that view the patient's information will be attacked | |
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

 
## Abuse Case 2 ##

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


## Misuse Case 1 ##

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
| Assumptions				| N/A	|
| Worst case threat			| The real patient is hard to find in the system 	|
| Capture Guaranteed		| The clerk should double check the information that he inputs |
| Potential Misuse Profile 	| Common |
| Related Business Rules	| BR1. System should support functions of correcting operation error |
| Stakeholder and Threats	| SH1: Employee: Employees will be confused about the duplicate patient information. Both may need to be updated when patient information changing <br> SH2: Hospital using this system: The reputation of the hospital will be damaged |
| Scope 					| Whole system 	|
| Abstraction Level 		| Misuser goal  |
| Precision level 			| Focused 		|


## Misuse Case 2 ##

| Column                	| Content |
| :---						| :---    |
| Misuse Case ID 			| Registration-M2 |
| Misuse Case Name 			| Wrong Information Provided by Patient  |
| Author					| Tam Nguyen |
| Date						| 10/01/2017 |
| Actor						| (Forgetful) Patient |
| Summary					| A patient unintentionally provides wrong information to the registration clerk during registration  |
| Basic Path				| BP0-1. The patient requests for being registered to the system <br> BP0-2. During the registration, for poor memory, the patient provides some wrong information like phone number to the clerk <br> BP0-3.The patient is registered with wrong information |
| Alternative Paths			| N/A |
| Capture Points			| CP1: (For BP0-2) The clerk double checks the information provided by the patient and corrects the error CP2: The patient recalls the correct information and asks clerks to correct it |
| Extension Points			| N/A	|
| Preconditions				| 1. The system including registration module run well <br> 2. No other connection problems like network or database connection  |
| Assumptions				| N/A	|
| Worst case threat			| The wrong patient information is created and used |
| Capture Guaranteed		| The wrong information is corrected during or after the registration, and not be used by anyone |
| Potential Misuse Profile 	| Common |
| Related Business Rules	| BR1. System should support functions of changing incorrect data <br> BR2. Employee should validate the data being recorded into the system  |
| Stakeholder and Threats	| SH1: Employees who use the wrong patient information may cause some problem and thus be punished <br> SH2: Hospital using this system: The reputation of the hospital will be damaged <br> SH3: Patient: With incorrect information, the patient may meet some problems like being unable to be contacted	|
| Scope 					| Whole system |
| Abstraction Level 		| Misuser goal  |
| Precision level 			| Focused |
