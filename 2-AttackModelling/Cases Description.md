#  Abuse/Misuse Cases #

## Diagram ##



## Abuse Case 1 ##

| Column                	| Content |
| :---						| :---    |
| Abuse Case ID 			| Registration-A2 |
| Abuse Case Name 			| Stored XSS |
| Author					| Xiangqing Ding |
| Date						| 10/01/2017 |
| Actors					| (Malicious) Registration Clerk |
| Summary					| A registration clerk puts some malicious Cross-site scripting when setting or editing patient's information. As a result, anyone who view the patient's page will suffer an XSS attack  |
| Basic Path				| BP0-1. The clerk logs into the openMRS system <br> BP0-2. The clerk goes to the patient registration module (by clicking "Register a Patient" button in the main page) <br> BP0-3. The clerk puts some XSS script in some information fields of the new patient (like "address")	<br> BP0-4. After completing the form, the clerk clicks the confirmation button to create the patient with XSS script <br> BP0-5.Anyone that view the patient's information will be attacked |
| Alternative Paths			| AP0-1. The clerk logs into the openMRS system <br> AP0-2. (Change step BP0-2) The clerk searches for an existing patient by clicking "Search a Patient" button <br> AP0-3. (Change step BP0-3) The clerk clicks the existing patient entry and puts some XSS script in some information fields	 <br> AP0-4. After completing the form, the clerk clicks the confirmation button to create the patient with XSS script <br> BP0-5.Anyone that view the patient's information will be attacked |
| Capture Points			| CP0-1: (For BP0-4) The script is not accepted. The clerk cannot create a user until the input is valid  <br> CP0-2: (For BP0-5) The script is accepted. But it cannot be executed for some mitigation techniques used in the system	|
| Extension Points			| N/A	|
| Exceptions				| N/A	|
| Preconditions				| 1. The system and registration module run well  |
| Assumptions				| 1. Whether the system is vulnerable to XSS attack (i.e. no corresponding mitigation or protection) is unknown		|
| Worst case threat			| The malicious script is stored in the system database with the patient's information. Any one who visit the patient's page will suffer an XSS attack	|
| Capture Guaranteed		| The script is not accepted or doesn't work |
| Potential Misuse Profile 	| Skilled. The clerk should at least have knowledge of website, XSS. |
| Scope 					| |
| Abstraction level 		| |
| Precision level 			| |


 
## Abuse Case 2 ##

| Column                	| Content |
| :---						| :---    |
| Abuse Case ID 			| Registration-A1 |
| Abuse Case Name 			| Interpolating Patients' Information |
| Author					| Zhuo Li |
| Date						| 10/01/2017 |
| Actors					| (Malicious) Registration Clerk |
| Summary					| A registration clerk changes the information of patients for a malicious purpose  |
| Basic Path				| BP0-1. The clerk logs into the openMRS system <br> BP0-2. The clerk goes to the patient registration module (by clicking "Register a Patient" button in the main page) <br> BP0-3. The clerk puts some XSS script in some information fields of the new patient (like "address")	<br> BP0-4. After completing the form, the clerk clicks the confirmation button to create the patient with XSS script <br> BP0-5.Anyone that view the patient's information will be attacked |
| Alternative Paths			| AP0-1. The clerk logs into the openMRS system <br> AP0-2. (Change step BP0-2) The clerk searches for an existing patient by clicking "Search a Patient" button <br> AP0-3. (Change step BP0-3) The clerk clicks the existing patient entry and puts some XSS script in some information fields	 <br> AP0-4. After completing the form, the clerk clicks the confirmation button to create the patient with XSS script <br> BP0-5.Anyone that view the patient's information will be attacked |
| Capture Points			| CP0-1: (For BP0-4) The script is not accepted. The clerk cannot create a user until the input is valid  <br> CP0-2: (For BP0-5) The script is accepted. But it cannot be executed for some mitigation techniques used in the system	|
| Extension Points			| N/A	|
| Exceptions				| N/A	|
| Preconditions				| 1. The system and registration module run well  |
| Assumptions				| 1. Whether the system is vulnerable to XSS attack (i.e. no corresponding mitigation or protection) is unknown		|
| Worst case threat			| The malicious script is stored in the system database with the patient's information. Any one who visit the patient's page will suffer an XSS attack	|
| Capture Guaranteed		| The script is not accepted or doesn't work |
| Potential Misuse Profile 	| Skilled. The clerk should at least have knowledge of website, XSS. |
| Scope 					| |
| Abstraction level 		| |
| Precision level 			| |


## Misuse Case 1 ##
## Misuse Case 2 ##