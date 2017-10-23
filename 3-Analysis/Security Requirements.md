# Security Requirements
`DESIGNER : Zhuo Li` <br/>
`EXECUTED BY : Zhuo Li` <br/>
`UPDATED ON : 22OCT17` <br/>
`EXECUTED ON : 22OCT17` <br/>

### SecReq01
Module:Manage Service Types

Requirements: Prevent the sysadmin from register a new service type which is the same as existing one. If the sysadmin register a existing one, the system should not register and generator some warning message.

Result: Pass

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq01.PNG)

### SecReq02
Module:Manage Service Types

Requirements: Prevent or remind the sysadmin from register a new service type which can last a extremely long time, e.g. 100000 min. It is meaningless for such a long time. If the sysadmin register a service type which last extremely long, the system should either remind the sysadmin “Do you want to register a 100000 min duration service type?” or just prevent the sysadmin and remind him “ you can not register a so long duration service type.”

Result: Failed. The duration for 100000 min is created successfully.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq02.PNG)

### SecReq03
Module:Manage Service Types

Requirements: The admin must can not change some service type to some existing service type.If the admin try to change some different service type, the system should prevent this behavior and warn the admin.

Result: Pass

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq03.PNG)


### SecReq04
Module:Manage Service Types

Requirements: The system should recognize different service type by the duration. If the differences of the two service type is time duration, that should be ok. Thus the system should allow the admin to register such a service type.

Result: Failed There isn't a service type Dermatology and duration 20min. It should be created.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq04.PNG)

### SecReq05
Module:Manage Service Types

Requirements: The system should only give the previlege to the admin to delete the service types. Especially if someone else try to delete the service type, the logging file should write down who did this without the system's preventing.

Result: Failed. The system allowed a clerk to delte the service type and logging file write the operation as an admin did.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq0501.PNG)
![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq0502.PNG)

### SecReq06
Module:Register a patient

Requirement: The system should validate the input for every field of the text. Especially for testing whether the input is malicious. If a user registerd with name in url format, the system should generate error message. Because this could cause XML injections or XSS Scripts.

Result: Failed

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq06.PNG)

### SecReq07
Module: Register a patient

Requirement: The application should validate the birth of date of the patient. If the user provide a invalid date of birth, the system should prevent that and generate a warning message. This validation aims at to valid the patient's information to avoid fake information.

Result: Pass

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq07.PNG)

### SecReq08
Module: Register a patient

Requirement: The system should authenticate the user when editing and saving the patient information. 
If the user has the previlege to do such things, there should be some log file to trace what the user did. These information should include userid, operation and timestamp at least. Then the new or changed data should be saved into the database. If user has no privilege to save the data, he should be redirected to an error page stating the error.

Result: Pass

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq08.PNG)

### SecReq09
Module:Register a patient

Requirement: The system should authorize the user's previlege every time when a user want to access a webpage. Especially when a user copy the url and try to access the webpage. If the user has the previlege, it is ok. If not, which means the user belongs to lower level of previlege, the system should prevent the user from accessing the webpage and generate a error page message. E.g. If user belongs to a lower privilege level and attempts to access higher privilege pages, for e.g. http://localhost:8082/openmrs-standalone/registrationapp/registerPatient.page?appId=referenceapplication.registrationapp.registerPatient 
the user should be redirected to error page.

Result: Failed. The nurse does not have the privilege to register a patient.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq09.PNG)


### SecReq10
Module:Register a patient

Requirement: The system should recognize there is already a patient which is similar to the one which is currently registering. If there is a patient who has the same first name and family name, the system should generate a remind message to avoid duplicate registering. This can avoid to generate too much useless record in the database.

Result: Pass

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq10.PNG)

