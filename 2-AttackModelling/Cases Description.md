#  Abuse/Misuse Cases #

## Diagram ##



## Abuse Case 1 ##
| Column                | Content |
| :---					| :---    |
| Abuse Case ID 		| Registration-A1 |
| Abuse Case Name 		| Stored XSS |
| Author				| Xiangqing Ding |
| Date					| 10/01/2017 |
| Actors				| Registration Clerk |
| Summary				| A registration clerk puts some malicious Cross-site scripting when setting or editing patient's information. As a result, anyone who view the patient's page will suffer an XSS attack  |

| Trigger				| 1. A registration clerk registering a new patient into the system <br> 2. A registration editing a existing patient information |
| Preconditions			| 1. The system and registration module run well <br> 2. The system is vulnerable to XSS attack (no corresponding protection) |
| Assumptions			|		|
| Post-conditions		| 1. The malicious script is stored in the system database with the patient's information. <br> Any one who visit the patient's page will suffer a XSS attack	|
| Basic Path			|		|
| Normal Flows			|		|
| Alternative Flows		|		|
| Exceptions			|		|
| Includes				|		|
| Frequency of Use		| 		|
| Special Requirements 	| 		|
| Note and Issues		|		|

 
## Abuse Case 2 ##
## Misuse Case 1 ##
## Misuse Case 2 ##