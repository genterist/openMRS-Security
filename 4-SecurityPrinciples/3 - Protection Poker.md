## Protection Poker ##


### Requirements ###

#### Overview ####
In this part we proposed five functional requirements. Those requirements may not be completely reasonable and necessary. They are designed for playing protection poker.

#### Requirement 1: Adding Message of Failing Logging in ####
To improve user experience, when user fails logging in and is redirected back to the logging page, there should be a failure message displayed on the logging page. To be visible enough to users, the font of the message should be larger than common text. In addition, the message should not be placed in the corner of the page and should be displayed in red. To be unambiguous to users, the message should be written in human language and contain the reason why logging in fails (e.g. "Wrong Username or Password").

#### Requirement 2: Adding Field of Driver License Number ####
To achieve better identification of patient, when registering new patient, the user could ask patient for his/her driver license number and input it to the system. Correspondingly, a new field for driver license number should be added to the Registering Page. This field should not be a necessary field.

#### Requirement 3: Better System Error Message ####
To prevent sensitive information being leaked, once the user meets a system error, the user interface should show the user appropriate error message instead of a stack/error trace which contain useful information about the application’s internal design, like java classes, libraries used or database table names. The message should be a summary of the error in human language without containing any sensitive information.


#### Requirement 4: Registering only at Registration Desk ####
To achieve better management, common users (e.g. clerk) with the ability of registering new patient could only register patients when logging in with location as "Registration Desk". Correspondingly, without logging in with selecting location as "Registration Desk", the "Register new Patient" button should not be accessible to users. However, the admin user could register a new patient everywhere.


#### Requirement 5: Removing Data Management Function ####
Since user could merge patients in the patient's page, the is no need of keeping "Data Management" module (The only function in this module is merging patients). The "Data Management" button should be no longer accessible to users in the main page. The ""Data Management" page should be removed.

### Database Table Value Points ###

Instead of using tables in this part, we used domains which organize the database tables in terms of the various information and also usage of the system.

| Domain			| Description		| Value		|
| :---              | :---      		| :--- 		|
| Concept | Concepts are defined and used to support strongly coded data throughout the system | |
| Encounter | Contains the meta-data regarding health care providers interventions with a patient | |
| Form | Essentially, the user interface description for the various components | |
| Observation | This is where the actual health care information is stored. There are many observations per Encounter | |
| Order | Things/actions that have been requested to occur | |
| Patient | Basic information about patients in this system | |
| User | Basic information about the people that use this system | |
| Person | Basic information about person in the system | |
| Business | Non medical data used to administrate openMRS | |
| Groups/Workflow | Workflows and Cohort data | |

Reference:  [https://wiki.openmrs.org/display/docs/Data+Model](https://wiki.openmrs.org/display/docs/Data+Model)

### Database Tables Used by Requirement ###

| Requirement		| Table Used	| Value Points of Table | Max Value |
| :---              | :---      	| :--- 					| :---		| 
| R1             |       	| 				| 		| 
| R2             |       	| 				| 		| 
| R3             |      	| 				| 		| 
| R4             |       	|  				| 		| 
| R5             |       	|  				| 		| 



### Security Ranking ###

| Requirement | Ease of Attack Points | Value of Asset Points | Security Risk | Rank of Security Risk |
| :---      | :---      			  | :--- 				  | :---			| :---		| 
| R1        | 	     			  	| 					  | 				| 			| 
| R2       	| 	     			  	| 	 				  | 				| 			|   
| R3      	| 	 					| 	 				  | 				| 			| 
| R4       	| 	      			  	| 	 				  | 				| 			| 
| R5       	| 	      			  	| 	 				  | 				| 			| 



### Explanation ###

