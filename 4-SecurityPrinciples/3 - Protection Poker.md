## Protection Poker ##


### Requirements ###

#### Overview ####
In this part we proposed five functional requirements for protection poker evaluation. Those requirements may not be completely reasonable and necessary.

#### Requirement 1: Adding Message of Failing Logging in ####
To improve user experience, when user fails logging in and is redirected back to the logging page, there should be a failure message displayed on the logging page. To be visible enough to users, the font of the message should be larger than common text. In addition, the message should not be placed in the corner of the page and should be displayed in red. To be unambiguous to users, the message should be written in human language and contain the reason why logging in fails (e.g. "Wrong Username or Password").

#### Requirement 2: Adding Field of Driver License Number ####
To achieve better identification of patient, when registering new patient, the user could ask patient for his/her driver license number and input it to the system. Correspondingly, a new field for driver license number should be added to the Registering Page. This field should not be a necessary field for registration.

#### Requirement 3: Better System Error Message ####
To prevent sensitive information being leaked, once the user meets a system error, the user interface should show the user appropriate error message instead of a stack/error trace which contain useful information about the application’s internal design, like java classes, libraries used or database table names. The message should be a summary of the error in human language without containing any sensitive information.


#### Requirement 4: Registering only at Registration Desk ####
To achieve better management, common users (e.g. clerk) with the ability of registering new patient could only register patients when logging in with location as "Registration Desk". Correspondingly, without logging in with selecting location as "Registration Desk", the "Register new Patient" button should not be accessible to users. However, the admin user could register a new patient everywhere.


#### Requirement 5: Removing Data Management Function ####
Since user could merge patients in the patient's page, the is no need of keeping "Data Management" module (The only function in this module is merging patients). The "Data Management" button should be no longer accessible to users in the main page. The ""Data Management" page should be removed.

### Database Domains Value Points ###

Instead of using tables in this part, we used domains which organize the database tables in terms of the various information and also usage of the system. The points to choose from: **[ 1, 2, 3, 5, 8, 13, 20, 40, 100 ]**.

| Domain			| Description		| Value		| 
| :---              | :---      		| :--- 		|
| Concept | Concepts are defined and used to support strongly coded data throughout the system | 40 |
| Encounter | Contains the meta-data regarding health care providers interventions with a patient. Some data like location are stored in this domain | 13 |
| Form | The user interface description for the various components. Not important but may contain some information could be used by attacker. | 13 |
| Observation | This is where the actual health care information is stored. This domain contains some private medical information like drug usage. | 20 |
| Order | Things/actions that have been requested to occur | 20 |
| Patient | Basic information about patients in this system. This domain does not contain much private information (which is actually stored in Person domain). So it may not be the most valuable one. | 40 |
| User | Basic information about the people that use this system. Username and password of system account are stored in this domain. | 100 |
| Person | Basic information about person in the system. Most private information such as address, mobile are stored in this domain. | 100 |
| Business | Non medical data used to administrate openMRS. This domain contains some data like report, which may contain sensitive data  | 20 |
| Groups/Workflow | Workflows and Cohort data | 8 |

Reference:  [https://wiki.openmrs.org/display/docs/Data+Model](https://wiki.openmrs.org/display/docs/Data+Model)

### Database Domains Used by Requirement ###

| Requirement		| Domain Used	| Value Sum |
| :---              | :---      	| :--- 	|
| R1             	| Form, Workflow 		| 26		|
| R2             	| Form, Patient, Person	| 156		| 
| R3             	| Form, Workflow 		| 21		| 
| R4             	| Form, Encounter 		| 26 		| 
| R5             	| Form		 			| 13 		| 



### Security Ranking ###

| Requirement | Ease of Attack Points | Value of Asset Points | Security Risk | Rank of Security Risk |
| :---      | :---      			| :--- 				  | :---			| :---		| 
| R1        | 	     	3		  	| 	26				  | 78				| 3			| 
| R2       	| 	     	13		  	| 	156				  | 2028			| 1			|   
| R3      	| 	 		1			| 	21 				  | 21				| 5			| 
| R4       	| 	      	2		  	| 	26				  | 52				| 4			| 
| R5       	| 	      	8		  	| 	13				  | 94				| 2			| 



### Explanation ###

To evaluate security risk of each requirement, the first step is evaluating values of different domains. How each domains is assigned is described in the **Description** column in the table of **Database Domains Value Points**. The value of asset points of each requirement is the sum of values of the domain it used. 

The ease of attack points of each requirement is decided by protection poker and discussions among group members. The points are also chosen from **[ 1, 2, 3, 5, 8, 13, 20, 40, 100 ]**. Among the five requirements, the 3rd requirement is selected as the hardest to attack. It removes detailed stack trace and uses appropriate error message. As a result, sensitive information contained in the stack trace could be avoided from being leaked. Thus it is assigned with 1 ease of attack point.

Starting from the 1st requirement, it adds UI elements in client side which could be integrated with malicious script. However, the content of the message is usually fixed and not related with user input. As a result, the ease of attack point should be about 3.
The 2nd requirement adds a new field (attack surface) of driver license number in registration page. Especially for the new field may not validate input as old fields, the attacker could easily inject malicious scripts via client side. However, considering the input validation in server side and Hibernate framework, the ease of attack point of this requirement is assigned with 13.
The 4th requirement doesn't increase or reduce attack surface. But considering that the implementation of the requirement may add some condition checking, breaking the condition checking may be one attack method. The ease of attack point of this requirement is assigned with 2.
The 5th requirement (Removing Data Management Function) reduces redundant pages (attack surfaces).  However, removing existing functionality and page may cause new vulnerability (e.g. exposed interface). Thus the ease of attack points is estimated to be 8.

In the end, the security risk can be calculated by **Security Risk = (Ease of Attack Points) * (Value of Asset Points)**. And the rank of security risk is assigned based on the security points.

