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
| Actors					| (Malicious) Registration Clerk |
| Summary					| A registration clerk puts some malicious cross-site scripting when setting or editing patient's information. As a result, anyone who view the patient's page will suffer an XSS attack  |
| Basic Path				| BP0-1. The clerk logs into the openMRS system <br> BP0-2. The clerk goes to the patient registration page and register a new patient <br> BP0-3. The clerk puts some XSS script in some information fields (like "address") of the new patient 	<br> BP0-4. After completing the form, the clerk clicks the confirmation button to create the patient <br> BP0-5.Anyone that view the patient's information will be attacked |
| Alternative Paths			| AP0-1. The clerk logs into the openMRS system <br> AP0-2. (Change step BP0-2) The clerk goes to the search page and searches for an existing patient <br> AP0-3. (Change step BP0-3) The clerk edits the information of the existing patient and puts some XSS script in some information fields	 <br> AP0-4. After completing the form, the clerk clicks the confirmation button to create the patient with XSS script  <br> BP0-5. Anyone that view the patient's information will be attacked |
| Capture Points			| CP0-1: (For BP0-4) The script is not accepted. The clerk cannot create a user until the input is valid  <br> CP0-2: (For BP0-5) The script is accepted. But it cannot be executed for some mitigation techniques used in the system	|
| Extension Points			| N/A	|
| Preconditions				| 1. The system and registration module run well  |
| Assumptions				| 1. Whether the system is vulnerable to XSS attack (i.e. no corresponding mitigation or protection) is unknown		|
| Worst case threat			| The malicious script is stored in the database and will be loaded when used. Anyone who visit the patient's page will suffer an XSS attack	|
| Capture Guaranteed		| The script is not accepted or doesn't work |
| Potential Misuse Profile 	| Skilled. The clerk should at least have some knowledge of web and XSS |
| Stakeholder and Threats	| SH1: Anyone who view the patient page	<br> T1-1:They will suffer XSS attack <br> SH2:Hospital using this system <br> T2-1: The reputation of the hospital will be damaged |
| Scope 					| Whole system |
| Abstraction level 		| Abuser goal  |

 
## Abuse Case 2 ##

| Column                	| Content |
| :---						| :---    |
| Abuse Case ID 			| Registration-A2 |
| Abuse Case Name 			| Interpolating Patients' Information |
| Author					| Zhuo Li |
| Date						| 10/01/2017 |
| Actors					| (Malicious) Registration Clerk |
| Summary					| A registration clerk changes the information of patients for some purpose  |
| Basic Path				| BP0-1. The clerk logs into the openMRS system <br> BP0-2. The clerk searches the patient he/she wants to to interpolate, and then goes to the page of the patient <br> BP0-3. The clerk interpolates the information of the patient without permission <br> BP0-4. After completing the form, the clerk clicks the confirmation button to confirm the change <br> BP0-5.The patient information has been changed |
| Alternative Paths			| N/A |
| Capture Points			| CP0-1: (For BP0-4) The clerk needs permission to change the information of patients	|
| Extension Points			| N/A	|
| Preconditions				| 1. The system and registration module run well  |
| Assumptions				| N/A	|
| Worst case threat			| The information of patient has been changed 	|
| Capture Guaranteed		| The clerk cannot change information of patient without permission |
| Potential Misuse Profile 	| Common. Knowing how to operate openMRS is enough |
| Stakeholder and Threats	| SH1: Patient <br> T1-1: Patient will meet troubles for unmatched information <br> 	SH2:Hospital using this system <br> T2-1: The reputation of the hospital will be damaged	|
| Scope 					| Whole system |
| Abstraction Level 		| Abuser goal  |


## Misuse Case 1 ##
## Misuse Case 2 ##